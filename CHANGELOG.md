# Changelog

Human-readable history of notable changes between releases. Git remains authoritative for exact diffs.

This file records **what changed between releases**. Test evidence belongs in [`docs/VALIDATION_HISTORY.md`](docs/VALIDATION_HISTORY.md) and [`docs/spikes/`](docs/spikes/); current and future work belongs in [`docs/ROADMAP.md`](docs/ROADMAP.md); durable design rationale belongs in [`docs/adr/`](docs/adr/). Cross-reference GitHub issues by number where one exists.

Format: newest release first, each as `## [x.y.z] - YYYY-MM-DD` with `Added`, `Changed`, `Fixed`, `Removed`, and `Documentation` subsections as needed. Collect unreleased work under `## [Unreleased]` and rename it when the release is cut. A project created from this template replaces the entries below with its own.

## [Unreleased]

### Added

- `tools/validate-package.sh` and a `Validate Package` GitHub Actions workflow that check package layout, `mod.info` identity and version, version drift across public text and runtime Lua, sandbox-option translations, package hygiene, and artwork.
- Root `workshop.txt` template, and a `.gitattributes` rule that keeps shell scripts LF.
- Project Zomboid-specific issue templates and an optional, commented-out `.github/FUNDING.yml`.
- A dated-entry format in `docs/VALIDATION_HISTORY.md` with a "Not covered" line, which also serves as the compatibility checkpoint after a Project Zomboid update, and a "Current development context" section in `AGENTS.md`.

### Changed

- Documentation consolidated from twelve docs and three root provenance files to eight docs and one provenance file, with a "known overlaps" section in `docs/DOCUMENTATION_OWNERSHIP.md` that says which file wins:
  - `docs/REQUIREMENTS.md` and `docs/ARCHITECTURE.md` → `docs/DESIGN.md` (separate Requirements and Architecture sections);
  - `docs/RELEASE_CHECKLIST.md`, `docs/STEAM_WORKSHOP.md`, and the rollback part of `docs/DEPLOYMENT.md` → `docs/RELEASING.md`, with one release checklist and no separate gates or decision record;
  - installation and configuration reference → the mod's own `README.md`;
  - `THIRD_PARTY_NOTICES.md` and `ASSET_LICENSE.md` → `CREDITS.md`;
  - `COMPLIANCE.md` → `docs/PZ_MODDING_POLICY.md`.
- Both placeholder `mod.info` files now use `modversion=` and carry `author=`, `category=`, and `versionMin=`; `42/mod.info` also references `icon=`. The package gains the Build 42 `common/` folder.
- `docs/TESTING.md` is a lean smoke/core/feature test set with normal-play logs accepted as evidence.
- `docs/DESIGN.md` documents the runtime layout and a build-stamp and version-handshake convention.
- `docs/adr/README.md` includes the ADR format, and the Workshop description template gains "What's new" and "Before you install" sections.
- `.gitignore` also ignores `DebugLog*/`, `server-console*.txt`, and `*.7z`.

### Removed

- The unused `source/` placeholder folder.
- The stable-release section of `docs/ROADMAP.md`, now owned by `docs/RELEASING.md`.

## [0.1.0] - 2026-08-28

- Initial Project Zomboid Build 42 repository template.
- Adds repository-local agent instructions, documentation ownership, compliance, validation, deployment, and release scaffolding.
