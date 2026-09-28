# Changelog

Human-readable history of notable changes between releases. Git remains authoritative for exact diffs.

This file records **what changed between releases**. Test evidence belongs in [`docs/VALIDATION_HISTORY.md`](docs/VALIDATION_HISTORY.md) and [`docs/spikes/`](docs/spikes/); current and future work belongs in [`docs/ROADMAP.md`](docs/ROADMAP.md); durable design rationale belongs in [`docs/adr/`](docs/adr/). Cross-reference GitHub issues by number where one exists.

Format: newest release first, each as `## [x.y.z] - YYYY-MM-DD` with `Added`, `Changed`, `Fixed`, `Removed`, and `Documentation` subsections as needed. Collect unreleased work under `## [Unreleased]` and rename it when the release is cut. A project created from this template replaces the entries below with its own.

## [Unreleased]

### Added

- `tools/validate-package.sh` and a `Validate Package` GitHub Actions workflow that check package layout, `mod.info` identity and version, version drift across public text and runtime Lua, sandbox-option translations, package hygiene, and artwork.
- Root `workshop.txt` template, and a `.gitattributes` rule that keeps shell scripts LF.
- Project Zomboid-specific issue templates and an optional, commented-out `.github/FUNDING.yml`.
- `docs/README.md` routing page, a compatibility-checkpoint template in `docs/VALIDATION_HISTORY.md`, and a "Current development context" section in `AGENTS.md`.

### Changed

- Both placeholder `mod.info` files now use `modversion=` and carry `author=`, `category=`, and `versionMin=`; `42/mod.info` also references `icon=`. The package gains the Build 42 `common/` folder.
- `docs/TESTING.md` and `docs/RELEASE_CHECKLIST.md` are restructured into a lean smoke/core/feature test set and general, stable, and deployment gates, with normal-play logs accepted as evidence.
- `docs/STEAM_WORKSHOP.md`, `docs/DEPLOYMENT.md`, and `docs/adr/README.md` are filled out with the structure used by shipped Build 42 mods, and the Workshop description template gains "What's new" and "Before you install" sections.
- `docs/ARCHITECTURE.md` documents the runtime layout and a build-stamp and version-handshake convention.
- `.gitignore` also ignores `DebugLog*/`, `server-console*.txt`, and `*.7z`.

## [0.1.0] - 2026-08-28

- Initial Project Zomboid Build 42 repository template.
- Adds repository-local agent instructions, documentation ownership, compliance, validation, deployment, and release scaffolding.
