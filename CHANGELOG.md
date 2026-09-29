# Changelog

Human-readable history of notable changes between releases. Git remains authoritative for exact diffs.

This file records **what changed between releases**. Test evidence belongs in [`docs/VALIDATION_HISTORY.md`](docs/VALIDATION_HISTORY.md) and [`docs/spikes/`](docs/spikes/); current and future work belongs in [`docs/ROADMAP.md`](docs/ROADMAP.md); durable design rationale belongs in [`docs/adr/`](docs/adr/). Cross-reference GitHub issues by number where one exists.

Format: newest release first, each as `## [x.y.z] - YYYY-MM-DD` with `Added`, `Changed`, `Fixed`, `Removed`, and `Documentation` subsections as needed. When server operators or players must do something after updating, such as re-enter a renamed sandbox option, add an `Upgrading` subsection that says what; [`docs/RELEASING.md`](docs/RELEASING.md#choosing-the-version-number) says how that affects the version number. Collect unreleased work under `## [Unreleased]` and rename it when the release is cut.

## How the template is versioned

> **When creating a mod from this template:** delete this section and every entry below it, and start with `## [Unreleased]`. The template's history is not the mod's history; the template's own `CHANGELOG.md` stays available upstream for later upgrades.

The template is released as `vX.Y.Z` git tags. The version number says what a release costs a mod that was already created from an earlier version:

| Increment | Meaning for an existing mod |
| --- | --- |
| Major (`X.0.0`), from `1.0.0` | Needs action: a document renamed or removed, a rule reversed, or a required step added. The `Upgrading` subsection says what to do |
| Minor (`X.Y.0`) | New optional guidance, checks, or files; adopt them when convenient. Before `1.0.0`, a minor release may also need action, and its `Upgrading` subsection then says so first |
| Patch (`X.Y.Z`) | Wording, clarification, or a fix inside the template. Nothing to act on |

Every minor or major release has an `Upgrading` subsection, even when it only says that nothing is required. A mod records the template version its files match under "Project facts" in `AGENTS.md`. To upgrade, read the `Upgrading` subsections of every later release, apply the ones that fit, and update that recorded version. `git diff v<recorded> v<latest>` in a clone of the template shows the exact changes.

## [Unreleased]

## [0.9.0] - 2026-09-28

### Added

- A "How to use this template" section at the top of `README.md`. It says the template assumes development with an AI coding agent but does not require one, gives the setup route and the way the agent finds its rules for Claude Code, another coding agent, and no agent, names the only Claude Code-specific files, and lists what to install.
- A "Running this interview with an agent" section in `docs/ADOPTION_INTERVIEW.md`, holding every rule for an agent that runs the interview: the check that the repository is not the template itself, asking one stage at a time, writing, the existing-mod ground rules, and landing. Any coding agent can now be told to follow it.
- Links from every file and folder in the README's repository map.

### Changed

- `.claude/commands/adopt.md` is now a short wrapper that tells Claude Code to follow the new interview section and reads `/adopt`'s argument. Its rules moved into the interview, so other agents get the same ones.
- The README's "Getting started" and "Restructure an existing mod" sections, the interview's "Before you start", and `AGENTS.md` describe running the interview with Claude Code, another agent, or by hand, and no longer assume Claude Code.

### Documentation

- An interview path for upgrading a mod created from an earlier template version is proposed in [#1](https://github.com/jonathanjacobs/pz-mod-template/issues/1) and not scheduled.

### Upgrading

Optional; nothing breaks without it. A mod that keeps `docs/ADOPTION_INTERVIEW.md` for later use can take the new version of it together with `.claude/commands/adopt.md`; the two must match, because the command now relies on the interview's agent section.

## [0.8.1] - 2026-09-28

### Documentation

- `README.md` opens with a table of contents, and its setup section is now "Getting started", with the shared first steps followed by "Start a new mod" and a new "Restructure an existing mod". The new section explains, before anyone runs `/adopt`, what the existing-mod path needs, what each step does, what happens to each kind of file, the two ways the result can land, and what never changes.

## [0.8.0] - 2026-09-28

### Changed

- New and existing mods now adopt the template the same way: create a repository with GitHub's "Use this template", then run `/adopt`. A new stage 0 in `docs/ADOPTION_INTERVIEW.md` asks whether the mod is new or an existing mod's repository being restructured, and for an existing mod, where that repository is.
- For an existing mod, three new stages replace the old gap-scan path. E1 reads the existing repository without changing it and records its package layout, Workshop ID, version, compatibility contracts, documents, license, and tooling, and stops for a Build 41-only mod. E2 plans what is copied as is, merged, replaced, or left out, and is confirmed before anything is copied. E3 copies the package tree byte for byte, checks it by comparing Git tree IDs, runs the three checks, and records every finding as a gap without changing the package. Stages 1 to 9 then start from what E1 found.
- A new stage 10 lands the result, by default as one pull request in the existing repository so its history, issues, and links survive, or by replacing that repository.
- `/adopt` stops when run in a clone of pz-mod-template itself, takes `existing <path or URL>` as an argument, never writes to the existing repository before stage 10, and never pushes, opens pull requests, or renames, archives, or deletes repositories.
- The README's setup section, `AGENTS.md`, and the folder indexes describe both paths.

### Removed

- The "Existing mods" gap-scan table and one-gap-at-a-time procedure in `docs/ADOPTION_INTERVIEW.md`.

### Upgrading

Optional; nothing breaks without it. A mod already set up needs none of this. To restructure an existing mod with the new path, start from a fresh repository created with "Use this template" at this version.

## [0.7.0] - 2026-09-28

### Added

- `docs/README.md`, an index of every document and folder in `docs/`, grouped by what it is used for, with the question each one answers.
- A rule in `AGENTS.md` to keep each folder's README current in the same commit that adds, removes, or renames something in that folder. It names the README for each folder: `docs/`, `tools/`, `.github/workflows/`, `.githooks/`, `.claude/`, the ADR and spike indexes, and the root repository map.
- Warnings in `tools/validate-package.sh` when a file or folder in `docs/` is missing from `docs/README.md`, or when that index links to something that does not exist.

### Upgrading

Optional; nothing breaks without it. Copy `docs/README.md` and remove the rows for documents the mod has deleted, add the README rule to "Verification expectations" in `AGENTS.md`, and take the "Documentation index" section of `tools/validate-package.sh`.

## [0.6.0] - 2026-09-28

### Changed

- `workshop-description.bbcode` moved from the repository root to `docs/workshop-description.bbcode`. `tools/validate-package.sh` checks it there, and warns when a copy is still at the root.
- Test logs, decompiled game source, and research material now live in local folders outside the repository. "Local files and automation" in `docs/TESTING.md` says so, explains how to give Claude Code access to those folders (`/add-dir`, or `permissions.additionalDirectories` in `.claude/settings.local.json`), and carries the test-cycle script suggestions and the remote-server settings layout that were in `scripts/README.md`. Test-cycle scripts now go in `tools/`.
- `.gitignore` keeps ignoring `Logs/`, `decompiled/`, and `research-source/`, in case copies are placed inside the repository, and now also ignores `*.java` and `*.class`.

### Removed

- The `Logs/`, `decompiled/`, and `research-source/` placeholder folders and their READMEs.
- `scripts/`, which held only a README of suggested scripts and `server.env.example`.
- The adoption interview's question about keeping decompiled source or research material, which only decided whether those folders were deleted.

### Upgrading

Action needed only with the new `tools/validate-package.sh`: move `workshop-description.bbcode` into `docs/` at the same time (`git mv workshop-description.bbcode docs/`), and fix links to it. Otherwise optional: move anything kept in `Logs/`, `decompiled/`, or `research-source/` to a folder outside the repository, delete those folders and `scripts/` if unused, and take the `.gitignore` lines.

## [0.5.0] - 2026-09-28

### Added

- `.github/pull_request_template.md`, which asks each pull request what was checked and what was skipped, whether it changes a compatibility contract or multiplayer authority, and whether it adds assets or third-party material.
- `.github/workflows/README.md`, which lists each workflow and job name for branch protection, and says why no README goes directly in `.github/`: GitHub would show it on the repository's front page in place of the root README.
- A "Do not update for" line at the top of each document in `docs/`, naming the information that looks as if it belongs there but has another home.
- A results table in `docs/VALIDATION_HISTORY.md`: `PASS`, `PASS with conditions`, `FAIL`, `INCOMPLETE`, and `NOT RUN`, given per check. Only the first two count as release evidence.
- A spike status table (`Open`, `GO`, `GO with conditions`, `NO-GO`, `Inconclusive`, `Superseded`), an index, and a record structure in `docs/spikes/README.md`. The structure asks for the GO and NO-GO criteria before any test runs, and the guidance asks for a NO-GO to be written up as carefully as a GO.
- Two evidence rules in `AGENTS.md`: a description of what a change should do is not evidence that it does, and every check is reported as passed, failed, or skipped.

### Changed

- The template-versioning table in this file now covers an optional addition released before `1.0.0`.
- `docs/ROADMAP.md` and `docs/VALIDATION_HISTORY.md` moved their "belongs elsewhere" sentences into the new opening line.

### Upgrading

Optional; nothing breaks without it. Copy `.github/pull_request_template.md` and `.github/workflows/README.md`, and take the results table from `docs/VALIDATION_HISTORY.md` and the status table and record structure from `docs/spikes/README.md`. Existing validation entries and spikes can keep their old result wording.

## [0.4.0] - 2026-09-28

### Added

- `docs/ADOPTION_INTERVIEW.md`, the setup steps as staged questions with the file each answer goes into. Stage 1 decides which later stages apply, and a separate path for an existing mod fills in a gap-scan table and then works one gap at a time without renaming anything published copies depend on. The `/adopt` command in `.claude/commands/adopt.md` has Claude Code ask the stages one at a time and write the answers, and `.claude/README.md` explains the folder.
- A Compatibility contracts section in `docs/DESIGN.md`: the kinds of names that saves, server settings, and other mods depend on (Mod ID, sandbox option names and defaults, ModData keys, command names, script full types, required Lua paths), why each matters, and a table for the mod's own.
- "Choosing the version number" in `docs/RELEASING.md`, which picks the increment by what an update does to existing worlds and servers, and a release-checklist item for contract changes.
- "How the template is versioned" in this file, and an `Upgrading` subsection for each template release, including 0.2.1 and 0.2.2.
- A "Template version" project fact and a replacement "Relationship to pz-mod-template" section in `AGENTS.md`, which say how to take template upgrades and how to report a general lesson back to the template repository.
- A README section on upgrading a mod created from an earlier template version.

### Changed

- `AGENTS.md` opens with a "Using this template" section that applies only during setup and is replaced afterward. It adds two working rules: treat compatibility contracts as fixed unless a task explicitly changes one, and keep file moves and renames in separate commits from behavior changes.
- The `CHANGELOG.md` format asks for an `Upgrading` subsection whenever players or server operators must act after an update.
- `.gitignore` excludes `.claude/settings.local.json`.

### Upgrading

Optional; nothing breaks without it. Add the two working rules under "Engineering boundaries" in `AGENTS.md`, the Compatibility contracts section of `docs/DESIGN.md`, and "Choosing the version number" in `docs/RELEASING.md`, then list the mod's existing contracts. Add a "Template version" line to the project facts in `AGENTS.md` set to the version the mod's files now match, and replace the opening paragraph of `AGENTS.md` with the "Relationship to pz-mod-template" section. `docs/ADOPTION_INTERVIEW.md` and `/adopt` are for setting up a mod; an existing mod can use their "Existing mods" path, then delete them.

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

### Upgrading

Optional; nothing breaks without it. Copy `tools/check-sensitive-content.sh`, `tools/check-lua-syntax.sh`, `.githooks/`, `.github/workflows/sensitive-content.yml`, and `docs/PRIVATE_DATA.md`, and take the `lua-syntax` job from `.github/workflows/validate-package.yml`. Run `bash tools/check-sensitive-content.sh` once over the whole repository before turning the workflow on: anything it finds in files that are already pushed is still in Git history, and the steps in `docs/PRIVATE_DATA.md` apply. Add the `.gitattributes` line for `.githooks/*` so the hook keeps LF line endings.

## [0.2.2] - 2026-09-28

### Added

- `CLAUDE.md`, which imports `AGENTS.md` so Claude Code reads the same agent instructions as other coding agents.

### Changed

- The `AGENTS.md` heading is now "Agent project handoff" rather than "Codex project handoff", since more than one coding agent reads it.

### Upgrading

For Claude Code users: add a root `CLAUDE.md` containing the line `@AGENTS.md`, or add that line to an existing `CLAUDE.md`. Claude Code reads `CLAUDE.md` in place of `AGENTS.md` when both exist.

## [0.2.1] - 2026-09-28

### Added

- A pz-mod-template attribution block in `NOTICE` (Copyright 2026 Jonathan Jacobs), which Apache 2.0 requires derived mods to keep in redistributions, with setup instructions in the README, `CREDITS.md`, and `AGENTS.md`, and a validator warning if it goes missing.
- An optional "Built with pz-mod-template" credit line in the Workshop description template and the suggested README sections.

### Upgrading

Recommended for a mod created from an earlier version: add a `NOTICE` file with the mod's own name and copyright at the top and the pz-mod-template block from this version's `NOTICE` below it.

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
