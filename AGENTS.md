# Codex project handoff

This repository is the starter workspace for a Project Zomboid mod. Before implementation begins, replace every `TBD` project fact below and keep this file tailored to the resulting mod.

## Privacy boundary

- Do not copy private assistant conversation content, titles, summaries, prompts, attachments, project metadata, or inferred personal context into this repository without explicit permission.
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
   - release gate: `docs/RELEASE_CHECKLIST.md`.
4. Treat reproducible tests and live Project Zomboid logs as stronger evidence than remembered API behavior or prior chat assertions.

## Project facts — complete before implementation

- Mod name: `TBD`
- Mod ID: `TBD`
- Steam Workshop ID: `TBD` (or `Not yet assigned`)
- Supported Project Zomboid build: `TBD`
- Primary multiplayer target: `TBD`
- Current development branch/release state: `TBD`

## Engineering boundaries

- Target only the Project Zomboid build(s) recorded in `VERSION`, `README.md`, and the canonical project docs.
- Preserve server authority for shared multiplayer state; explicitly document any client-only behavior.
- Avoid patching Project Zomboid Java/core files for ordinary Workshop distribution.
- Do not copy third-party mod code or artwork without verified permission. Record any permitted material in `THIRD_PARTY_NOTICES.md` and `ASSET_LICENSE.md` before distribution.
- Keep diagnostics off or low-volume by default; enable verbose logging only for focused evidence windows.
- Do not claim compatibility, performance, or release readiness beyond collected evidence.
- Keep the deployable mod tree under `Contents/mods/<mod-id>/`; do not package source-control metadata, saves, logs, private configuration, decompiled source, or extracted game assets.

## Verification expectations

- When package structure, `mod.info`, sandbox options, translations, or required Lua modules change, run the applicable validation workflow before claiming success.
- For runtime changes, update `docs/TESTING.md` before or with the implementation; add an entry to `docs/VALIDATION_HISTORY.md` only after a real test occurs.
- Use a spike document for bounded uncertainty or feasibility research. Promote conclusions into requirements, architecture, or an ADR only after evidence supports them.
- Recheck `git diff` for generated files, logs, server saves, Workshop artifacts, private configuration, and accidental Project Zomboid/third-party assets before committing.
