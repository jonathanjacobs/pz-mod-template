# Codex project handoff

This repository is the starter workspace for a Project Zomboid mod. Before implementation begins, replace every `TBD` project fact below and keep this file tailored to the resulting mod.

## Privacy boundary

- Do not copy private assistant conversation content, titles, summaries, prompts, attachments, project metadata, inferred personal context, logs, or private game/server data into this repository without explicit permission.
- Do not add persona-identifying or personal information without an explicit request.
- Translate permitted requirements into impersonal, repository-native technical language.
- Apply this rule to source, docs, comments, commit messages, fixtures, logs, generated artifacts, and issue or pull-request text.

## Start every task here

1. Run `git status --short --branch` and preserve unrelated user changes.
2. Read `docs/DOCUMENTATION_OWNERSHIP.md` before changing documentation.
3. Use the canonical document for the subject being changed:
   - behavior: `docs/REQUIREMENTS.md`;
   - implementation: `docs/ARCHITECTURE.md` and `docs/adr/`;
   - planned work and release gates: `docs/ROADMAP.md`;
   - test procedure: `docs/TESTING.md`;
   - completed evidence: `docs/VALIDATION_HISTORY.md`;
   - experiments: `docs/spikes/`;
   - deployment and rollback: `docs/DEPLOYMENT.md`;
   - Workshop publication: `docs/STEAM_WORKSHOP.md`;
   - release gate: `docs/RELEASE_CHECKLIST.md`;
   - external reference links: `docs/RESEARCH_LINKS.md`.
4. Treat reproducible tests and live Project Zomboid logs as stronger evidence than remembered API behavior or prior chat assertions. Before interpreting any test or log, confirm the client and server ran the same package (see the build-stamp convention in `docs/ARCHITECTURE.md`); duplicate local and Workshop copies with the same Mod ID can load mixed Lua and sandbox-option versions.

## Project facts — complete before implementation

- Mod name: `TBD`
- Mod ID: `TBD`
- Steam Workshop ID: `TBD` (or `Not yet assigned`)
- Supported Project Zomboid build: `TBD`
- Primary multiplayer target: `TBD`
- Current development branch/release state: `TBD`

## Current development context

Keep this section short and current. Record what an agent starting cold must know that the code does not show: which branches are live and what each is for, which behavior has evidence and which does not yet, and any environment trap that has already produced a misleading result. Do not represent unproven behavior as proven here.

- `TBD`

## Engineering boundaries

- Target only the Project Zomboid build(s) recorded in `VERSION`, `README.md`, and the canonical project docs.
- Preserve server authority for shared multiplayer state; explicitly document any client-only behavior.
- Avoid patching Project Zomboid Java/core files for ordinary Workshop distribution.
- Do not copy third-party mod code or artwork without verified permission. Record any permitted material in `THIRD_PARTY_NOTICES.md` and `ASSET_LICENSE.md` before distribution.
- Keep diagnostics off or low-volume by default; enable verbose logging only for focused evidence windows.
- Do not claim compatibility, performance, or release readiness beyond collected evidence.
- Keep the deployable mod tree under `Contents/mods/<mod-id>/`; do not package source-control metadata, saves, logs, private configuration, decompiled source, or extracted game assets.
- Write in American English (`behavior`, `authorize`, `neighbor`, `judgment`) in documentation, code comments, commit messages, and GitHub issues and issue comments. This does not extend to code: engine API names are spelled as Project Zomboid defines them, and several are British (`initialise()` on `ISUIElement`, for example). Never apply a spelling change to source files by blanket search and replace — a sweep that does exactly that can rename call sites and break working code. Correct spelling in prose by hand, and leave identifiers alone.
- Never hard-wrap markdown paragraphs. Write each paragraph as one unwrapped line and let the renderer wrap it. This applies to repository documents, GitHub issue bodies, issue comments, and pull request descriptions — GitHub renders those with hard line breaks enabled, so a newline inside a paragraph becomes a literal forced break when the window is resized. Fenced code blocks and table rows keep their own line structure.
- Track open defects and design questions as GitHub Issues once the repository has an issue tracker in use; cross-reference by issue number in `CHANGELOG.md`, `docs/ROADMAP.md`, and `docs/VALIDATION_HISTORY.md` entries so history stays navigable.

## Verification expectations

- When package structure, `mod.info`, sandbox options, translations, version strings, or required Lua modules change, run `bash tools/validate-package.sh` (the same check CI runs) before claiming success. When a regression is fixed, consider adding a guard for it to that script.
- Keep `VERSION`, the `modversion=` line in every `mod.info`, and any version reference in `README.md` aligned on every bump. Grep the repository for the previous version string rather than relying on memory of "the usual few spots" — a check that only covers some of the locations will eventually miss one and let them drift.
- If this repository has `scripts/` test-cycle automation (see `scripts/README.md`), use it for the mod-deploy and log-capture steps around a test run rather than repeating them by hand.
- For runtime changes, update `docs/TESTING.md` before or with the implementation; add an entry to `docs/VALIDATION_HISTORY.md` only after a real test occurs.
- Use a spike document for bounded uncertainty or feasibility research. Promote conclusions into requirements, architecture, or an ADR only after evidence supports them.
- Recheck `git diff` for generated files, logs, server saves, Workshop artifacts, private configuration, and accidental Project Zomboid/third-party assets before committing.
