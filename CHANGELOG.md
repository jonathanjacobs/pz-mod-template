# Changelog

Human-readable history of notable changes between releases. Git remains authoritative for exact diffs.

This file records **what changed between releases**. Test evidence belongs in [`docs/VALIDATION_HISTORY.md`](docs/VALIDATION_HISTORY.md) and [`docs/spikes/`](docs/spikes/); current and future work belongs in [`docs/ROADMAP.md`](docs/ROADMAP.md); durable design rationale belongs in [`docs/adr/`](docs/adr/). Cross-reference GitHub issues by number where one exists.

Format: newest release first, each as `## [x.y.z] - YYYY-MM-DD` with `Added`, `Changed`, `Fixed`, `Removed`, and `Documentation` subsections as needed. Collect unreleased work under `## [Unreleased]` and rename it when the release is cut. A project created from this template replaces the entries below with its own.

## [Unreleased]

## [0.3.0] - 2026-09-28

### Added

- `docs/PRIVATE_DATA.md`, which lists the server, player, and credential details that never enter the repository or its GitHub pages (server IP addresses and host names, Steam IDs, other players' names, server, admin, and RCON passwords, SFTP credentials, tokens), says to describe test environments by kind, and gives the steps to take after a leak. Those steps include the GitHub behavior that makes a history rewrite insufficient: old commits stay viewable at their direct URLs after a force-push until GitHub Support purges them.
- `tools/check-sensitive-content.sh`, run by a new `Sensitive Content` workflow on tracked files, pull request text, and commit messages, and by an optional pre-commit hook in `.githooks/` (`git config core.hooksPath .githooks`). It fails on IPv4 addresses outside the loopback and documentation ranges, SteamID64 values, filled-in server password settings and `*PASSWORD=`/`*TOKEN=` lines, credentials in URLs, GitHub tokens, and tracked `.env`, `.pem`, `.ppk`, and SSH key files. Project-specific patterns such as player names go in a `SENSITIVE_PATTERNS` repository secret, and a `sensitive-content: allow` marker accepts a false positive.
- `tools/check-lua-syntax.sh` and a "Check Lua syntax" job in the `Validate Package` workflow, which checks that every tracked `.lua` file parses as Lua 5.1 so syntax errors show up without launching the game. Locally it reports the check as skipped when no Lua 5.1 compiler is installed.
- `.gitignore` entries for `*.env`, `*.pem`, `*.ppk`, and SSH private keys.

### Changed

- `AGENTS.md` names the private details to keep out, points to `docs/PRIVATE_DATA.md`, and asks agents to run both new checks and to report a skipped check as skipped.
- The validation-history entry format, spike guidance, `docs/TESTING.md`, `scripts/README.md`, and the release checklist now point to the private-details rules where log excerpts and server details are written down.
- Both workflows declare read-only `contents` permission and use `actions/checkout@v6`.

### Upgrading a mod created from 0.2.x

Copy `tools/check-sensitive-content.sh`, `tools/check-lua-syntax.sh`, `.githooks/`, `.github/workflows/sensitive-content.yml`, and `docs/PRIVATE_DATA.md`, and take the `lua-syntax` job from `.github/workflows/validate-package.yml`. Run `bash tools/check-sensitive-content.sh` once over the whole repository before turning the workflow on: anything it finds in files that are already pushed is still in Git history, and the steps in `docs/PRIVATE_DATA.md` apply. Add the `.gitattributes` line for `.githooks/*` so the hook keeps LF line endings.

## [0.2.2] - 2026-09-28

### Added

- `CLAUDE.md`, which imports `AGENTS.md` so Claude Code reads the same agent instructions as other coding agents.

### Changed

- The `AGENTS.md` heading is now "Agent project handoff" rather than "Codex project handoff", since more than one coding agent reads it.

## [0.2.1] - 2026-09-28

### Added

- A pz-mod-template attribution block in `NOTICE` (Copyright 2026 Jonathan Jacobs), which Apache 2.0 requires derived mods to keep in redistributions, with setup instructions in the README, `CREDITS.md`, and `AGENTS.md`, and a validator warning if it goes missing.
- An optional "Built with pz-mod-template" credit line in the Workshop description template and the suggested README sections.

## [0.2.0] - 2026-09-28

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
