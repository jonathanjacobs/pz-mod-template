# Project Zomboid Mod Template

Starter repository for an independent Project Zomboid mod. Use this repository as a Git template, then replace the `TBD` values and remove any scaffolding that has no job in the new project.

Status: **Template / not a deployable mod**  
Template version: **v0.1.0**  
Target baseline: **Project Zomboid Build 42 (confirm the exact version per project)**

## Why this template looks the way it does

This is more scaffolding than a small mod strictly needs on day one, and that is intentional. The target workflow is many development sessions — often with an AI coding agent — spread across weeks or months, where nothing survives between sessions except what is written down in this repository. `docs/VALIDATION_HISTORY.md`'s evidence discipline and `docs/DOCUMENTATION_OWNERSHIP.md`'s single-source-of-truth rule exist specifically to stop a long-running project from drifting into unsupported claims or duplicated, contradicting facts across files — the docs function as the project's durable memory, re-read at the start of each session rather than trusted to anyone's recollection.

If a project is short-lived or exploratory, most of this can be ignored or deleted; see the repository map below for what is core versus optional. If it is going to run for months across many sessions, keep the discipline — it is what makes that possible.

## Start a new mod

1. Create a repository from this template.
2. Rename the placeholder directory at `Contents/mods/pz-mod-id/` to the chosen stable Mod ID.
3. Replace the placeholder values in `AGENTS.md`, `VERSION`, both `Contents/mods/<mod-id>/mod.info` files (including `author=` and `versionMin=`; see [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md#runtime-layout)), and the core project docs.
4. Define the first deliverable in `docs/REQUIREMENTS.md` and plan it in `docs/ROADMAP.md`.
5. Remove unused optional scaffolding rather than maintaining empty paperwork.

## Repository map

### Core — keep from day one

- `AGENTS.md` — development handoff and working rules.
- `Contents/mods/` — deployable Project Zomboid mod package(s).
- `VERSION`, `CHANGELOG.md` — release identity.
- `LICENSE`, `NOTICE` — the template's own licensing.
- `COMPLIANCE.md`, `docs/PZ_MODDING_POLICY.md` — modding-policy rules that apply from the first commit, not just at release.
- `docs/DOCUMENTATION_OWNERSHIP.md` — authoritative document map and update rules.
- `docs/REQUIREMENTS.md` — normative behavior.
- `docs/ARCHITECTURE.md` — implementation design.

### Grows with the project — start as a stub, fill in as work happens

- `docs/ROADMAP.md` — planned work and milestones.
- `docs/TESTING.md` — repeatable test procedure.
- `docs/VALIDATION_HISTORY.md` — actual test outcomes.
- `docs/adr/` — durable technical decision records, once a decision has real alternatives.
- `docs/spikes/` — bounded feasibility investigations, once one is needed.
- `docs/DEPLOYMENT.md` — packaging, install, and rollback, once there's something to install.
- `THIRD_PARTY_NOTICES.md`, `ASSET_LICENSE.md` — provenance records, filled in as third-party or non-code material is added.

### Pre-release / Workshop-publication only — dormant until you're preparing to ship

- `docs/RELEASE_CHECKLIST.md` — the release gate.
- `docs/STEAM_WORKSHOP.md`, `workshop-description.bbcode` — Workshop publication; leave as a stub or remove if not publishing there.

### Fully optional — delete freely if you don't use the workflow

- `docs/RESEARCH_LINKS.md` — external reference links, if tracking them helps.
- `scripts/` — test-cycle automation; see `scripts/README.md`.
- `Logs/`, `decompiled/`, `research-source/` — gitignored working directories for test logs, decompiled engine source, and external research material; see each folder's README.
- `tools/` — shared tools, only if something is genuinely reusable across the repository.

## Documentation map

Read [`docs/DOCUMENTATION_OWNERSHIP.md`](docs/DOCUMENTATION_OWNERSHIP.md) for the complete source-of-truth map. Keep this README focused on orientation; do not turn it into the project governance manual.

## License and status

The template's original material is licensed under Apache-2.0. Project Zomboid code and assets remain property of their respective owners and are neither redistributed nor relicensed here. A project created from this template is an unofficial independent community mod unless documented otherwise.
