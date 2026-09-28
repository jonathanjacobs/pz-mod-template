# Shared tools

Add a tool here only when it is genuinely reusable across this repository. Document its prerequisites, inputs, outputs, and how to run it. Do not add generated release output to this directory.

## `validate-package.sh`

Checks the deployable package and the public text that describes it. CI runs it on every push and pull request to `main` through [`../.github/workflows/validate-package.yml`](../.github/workflows/validate-package.yml); run it locally before committing a version bump, package-structure change, sandbox option, or translation.

```bash
bash tools/validate-package.sh
```

Prerequisites: bash with `grep`, `sed`, `awk`, `od`, and `stat` (Git Bash on Windows is enough). An optional argument names a different repository root. The script prints one line per problem and exits non-zero on any error; warnings do not fail it.

It always checks:

- exactly one mod under `Contents/mods/`, a `common/` and `42/` folder, and no stray root-level runtime copy;
- both `mod.info` files: `id=` matches the folder, `modversion=` matches `VERSION`, no legacy `version=` key, and `42/mod.info` has `versionMin=`;
- version drift: bold `**vX.Y.Z**` labels in `README.md`, `[b]Version:[/b]` in `workshop-description.bbcode`, `vX.Y.Z` in the `workshop.txt` description, and runtime Lua build stamps (`BUILD_VERSION = "X.Y.Z"`, `buildVersion = "X.Y.Z"`, `Loaded vX.Y.Z`) must all match `VERSION`;
- every sandbox option has a `translation =` line with an EN `Sandbox_<key>` label (JSON or `Sandbox_EN.txt`), and every sandbox page has a label;
- no logs, backups, archives, `.env` files, or Java sources/classes inside the package;
- `NOTICE` still carries the pz-mod-template attribution block (a warning, never an error);
- `[center]` and `[br]` in the Workshop description, which Steam does not render;
- PNG identity of any artwork present, and `preview.png` at 256×256 and at most 1000 KB.

Once `workshop.txt` has a numeric `id=`, it also requires `preview.png` and the `poster=`/`icon=` files named in `42/mod.info`, and rejects leftover `[PLACEHOLDER]` text in the Workshop description.

Add project-specific regression guards in the marked section near the end of the script. Add a guard only for a defect or design boundary that has already mattered once, and comment what it protects.
