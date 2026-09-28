# Project Zomboid Mod Template

Starter repository for an independent Project Zomboid mod. Use this repository as a Git template, then replace the `TBD` values and remove any scaffolding that has no job in the new project.

Status: **Template / not a deployable mod**  
Template version: **v0.3.0**  
Target baseline: **Project Zomboid Build 42 (confirm the exact version per project)**

## Why this template looks the way it does

The target workflow is many development sessions — often with an AI coding agent — spread across weeks or months, where nothing survives between sessions except what is written down in this repository. The docs are the project's durable memory, re-read at the start of each session rather than trusted to anyone's recollection. `docs/VALIDATION_HISTORY.md`'s evidence discipline and `docs/DOCUMENTATION_OWNERSHIP.md`'s single-source-of-truth rule exist to stop a long-running project from drifting into unsupported claims or contradicting copies of the same fact.

The template keeps that discipline in as few documents as possible: one file per concern, each with a clear owner, and automated checks (the scripts in `tools/`) doing the work that would otherwise be a manual checklist.

## Start a new mod

1. Create a repository from this template.
2. Rename the placeholder directory at `Contents/mods/pz-mod-id/` to the chosen stable Mod ID.
3. Replace the placeholder values in `AGENTS.md`, `VERSION`, both `Contents/mods/<mod-id>/mod.info` files (including `author=` and `versionMin=`; see [`docs/DESIGN.md`](docs/DESIGN.md#runtime-layout)), and `workshop.txt`.
4. Replace this README with the mod's own. Suggested sections: what it does, installation and server setup (`WorkshopItems=` / `Mods=`), configuration reference with safe defaults, compatibility, uninstalling, links to the docs, and a closing credit line: "Built with [pz-mod-template](https://github.com/jonathanjacobs/pz-mod-template)."
5. Add the mod's own name and copyright at the top of `NOTICE`, above the pz-mod-template block, and keep that block. Apache 2.0 requires it to stay in the `NOTICE` file of anything redistributed from this repository.
6. Define the first deliverable in `docs/DESIGN.md` and plan it in `docs/ROADMAP.md`.
7. Turn on the pre-commit check for private details, once per clone: `git config core.hooksPath .githooks`. See [`docs/PRIVATE_DATA.md`](docs/PRIVATE_DATA.md) for what it catches.
8. Run `bash tools/validate-package.sh`; the remaining warnings list what is still a placeholder.

## Repository map

### Core — keep from day one

- `AGENTS.md` — development handoff and working rules. `CLAUDE.md` imports it for Claude Code, so both tools read the same rules.
- `Contents/mods/` — deployable Project Zomboid mod package.
- `VERSION`, `CHANGELOG.md` — release identity.
- `LICENSE`, `NOTICE` — licensing.
- `docs/PZ_MODDING_POLICY.md`, `CREDITS.md` — modding-policy rules and asset/third-party provenance, which apply from the first commit, not just at release.
- `docs/PRIVATE_DATA.md` — server, player, and credential details that never enter the repository or its GitHub pages, and what to do if one does.
- `docs/DOCUMENTATION_OWNERSHIP.md` — which document owns which fact.
- `docs/DESIGN.md` — requirements and architecture.
- `docs/ROADMAP.md` — milestones and current work.
- `docs/TESTING.md` — repeatable test procedure.
- `docs/VALIDATION_HISTORY.md` — actual test outcomes.
- `tools/`, `.github/workflows/`, `.githooks/` — automated checks for the package and version drift, Lua syntax, and private details, run locally, in CI, and (once turned on) before each commit; see `tools/README.md`.

### Add when needed

- `docs/adr/` — durable decision records, once a decision has real alternatives.
- `docs/spikes/` — bounded feasibility investigations, once engine behavior needs an experiment.
- `docs/RELEASING.md`, `workshop.txt`, `workshop-description.bbcode` — release checklist, Workshop publication, and rollback. Add `preview.png` at the root before the first upload; remove the Workshop files if not publishing there.

### Optional — delete freely if you don't use the workflow

- `docs/RESEARCH_LINKS.md` — external reference links and mods studied for ideas.
- `.github/ISSUE_TEMPLATE/`, `.github/FUNDING.yml` — Project Zomboid-specific issue templates and optional sponsor links; the funding file is all comments until filled in.
- `scripts/` — test-cycle automation; see `scripts/README.md`.
- `Logs/`, `decompiled/`, `research-source/` — gitignored working directories for test logs, decompiled engine source, and external research material; see each folder's README.

## License and status

The template's original material is Copyright 2026 Jonathan Jacobs and licensed under Apache-2.0; see [`NOTICE`](NOTICE). Project Zomboid code and assets remain property of their respective owners and are neither redistributed nor relicensed here. A project created from this template is an unofficial independent community mod unless documented otherwise.
