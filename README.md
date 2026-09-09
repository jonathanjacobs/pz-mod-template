# Project Zomboid Mod Template

Starter repository for an independent Project Zomboid mod. Use this repository as a Git template, then replace the `TBD` values and remove any scaffolding that has no job in the new project.

Status: **Template / not a deployable mod**  
Template version: **v0.1.0**  
Target baseline: **Project Zomboid Build 42 (confirm the exact version per project)**

## Start a new mod

1. Create a repository from this template.
2. Rename the placeholder directory at `Contents/mods/pz-mod-id/` to the chosen stable Mod ID.
3. Replace the placeholder values in `AGENTS.md`, `VERSION`, `Contents/mods/<mod-id>/mod.info`, and the core project docs.
4. Define the first deliverable in `docs/REQUIREMENTS.md` and plan it in `docs/ROADMAP.md`.
5. Remove unused optional scaffolding rather than maintaining empty paperwork.

## Repository map

- `AGENTS.md` — development handoff and working rules.
- `Contents/mods/` — deployable Project Zomboid mod package(s).
- `docs/DOCUMENTATION_OWNERSHIP.md` — authoritative document map and update rules.
- `docs/` — requirements, architecture, testing, validation, deployment, and release controls.
- `docs/adr/` — durable technical decision records, when needed.
- `docs/spikes/` — bounded feasibility investigations, when needed.
- `docs/RESEARCH_LINKS.md` — external reference links, when tracked.
- `scripts/` — optional test-cycle automation; see `scripts/README.md`. Remove if unused.
- `Logs/`, `decompiled/`, `research-source/` — optional gitignored working directories for test logs, decompiled engine source, and external research material; see each folder's README. Remove if unused.
- `CHANGELOG.md`, `VERSION`, and release/legal files — public release identity and provenance controls.

## Documentation map

Read [`docs/DOCUMENTATION_OWNERSHIP.md`](docs/DOCUMENTATION_OWNERSHIP.md) for the complete source-of-truth map. Keep this README focused on orientation; do not turn it into the project governance manual.

## License and status

The template's original material is licensed under Apache-2.0. Project Zomboid code and assets remain property of their respective owners and are neither redistributed nor relicensed here. A project created from this template is an unofficial independent community mod unless documented otherwise.
