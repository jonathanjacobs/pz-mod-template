# Project Zomboid Mod Template

Starter repository for an independent Project Zomboid mod. Use it as a Git template to start a new mod, or to restructure an existing mod's repository, then replace the `TBD` values and remove any scaffolding that has no job in the mod.

Status: **Template / not a deployable mod**  
Template version: **v0.9.0**  
Target baseline: **Project Zomboid Build 42 (confirm the exact version per project)**

## Contents

- [How to use this template](#how-to-use-this-template)
- [Why this template looks the way it does](#why-this-template-looks-the-way-it-does)
- [Getting started](#getting-started)
  - [Start a new mod](#start-a-new-mod)
  - [Restructure an existing mod](#restructure-an-existing-mod)
- [Upgrading a mod created from an earlier template version](#upgrading-a-mod-created-from-an-earlier-template-version)
- [Repository map](#repository-map)
- [License and status](#license-and-status)

## How to use this template

This template assumes most of the mod's development happens together with an AI coding agent: a tool such as Claude Code, OpenAI Codex, GitHub Copilot, Cursor, or Gemini CLI that reads and edits the repository on your instructions. An agent remembers nothing between sessions, so the documents here are written to be the project's memory, and [`AGENTS.md`](AGENTS.md) holds the working rules every agent reads first.

Nothing requires an agent. The documents are plain Markdown, the checks are bash scripts, and CI runs on GitHub. Without an agent you read and fill in more yourself, and `AGENTS.md` still describes the project's conventions.

| You work with | To set up a mod | How the agent finds the rules |
| --- | --- | --- |
| Claude Code | Run `/adopt`: a command typed at the Claude Code prompt, which runs the instructions in [`.claude/commands/adopt.md`](.claude/commands/adopt.md) | [`CLAUDE.md`](CLAUDE.md) imports `AGENTS.md` into every session |
| Another coding agent | Ask it to run the adoption interview in [`docs/ADOPTION_INTERVIEW.md`](docs/ADOPTION_INTERVIEW.md), following its section "Running this interview with an agent" | Many agents read `AGENTS.md` on their own. If yours does not, tell it to read `AGENTS.md` at the start of each session |
| No AI assistant | Work through [`docs/ADOPTION_INTERVIEW.md`](docs/ADOPTION_INTERVIEW.md) yourself, or follow the checklist under [Start a new mod](#start-a-new-mod) | Not applicable |

Only `CLAUDE.md` and `.claude/` are specific to Claude Code. Delete both if you do not use it.

**What you need:**

- a GitHub account, for "Use this template" and the checks that run on every push and pull request;
- Git;
- bash, to run the scripts in `tools/`: built into macOS and Linux, and included with Git for Windows as Git Bash;
- Project Zomboid Build 42, for testing the mod;
- optionally, a Lua 5.1 compiler (`luac5.1`) to check Lua syntax locally; CI checks it either way;
- optionally, a coding agent.

## Why this template looks the way it does

The target workflow is many development sessions — often with an AI coding agent — spread across weeks or months, where nothing survives between sessions except what is written down in this repository. The docs are the project's durable memory, re-read at the start of each session rather than trusted to anyone's recollection. `docs/VALIDATION_HISTORY.md`'s evidence discipline and `docs/DOCUMENTATION_OWNERSHIP.md`'s single-source-of-truth rule exist to stop a long-running project from drifting into unsupported claims or contradicting copies of the same fact.

The template keeps that discipline in as few documents as possible: one file per concern, each with a clear owner, and automated checks (the scripts in `tools/`) doing the work that would otherwise be a manual checklist.

## Getting started

New and existing mods start the same way:

1. On GitHub, choose **Use this template → Create a new repository**. This gives you a repository of your own without the template's history.
2. Clone the new repository.
3. Start the adoption interview in the way that fits [how you work](#how-to-use-this-template): `/adopt` in Claude Code, a request to another coding agent, or by hand. Its first question is whether this is a new mod or an existing mod's repository being restructured.

The interview in [`docs/ADOPTION_INTERVIEW.md`](docs/ADOPTION_INTERVIEW.md) asks its questions one stage at a time and names the file each answer goes into. An agent running it shows each change before making it. Do not run the interview in a clone of this template itself; an agent following it stops if you try.

### Start a new mod

The interview asks which kind of mod this is (single-player or multiplayer, published on the Workshop or not), then only the questions that apply. A small single-player mod takes about twenty minutes. The same setup as a checklist:

1. Create a repository from this template.
2. Rename the placeholder directory at `Contents/mods/pz-mod-id/` to the chosen stable Mod ID.
3. Replace the placeholder values in `AGENTS.md`, `VERSION`, both `Contents/mods/<mod-id>/mod.info` files (including `author=` and `versionMin=`; see [`docs/DESIGN.md`](docs/DESIGN.md#runtime-layout)), and `workshop.txt`.
4. Replace this README with the mod's own. Suggested sections: what it does, installation and server setup (`WorkshopItems=` / `Mods=`), configuration reference with safe defaults, compatibility, uninstalling, links to the docs, and a closing credit line: "Built with [pz-mod-template](https://github.com/jonathanjacobs/pz-mod-template)."
5. Add the mod's own name and copyright at the top of `NOTICE`, above the pz-mod-template block, and keep that block. Apache 2.0 requires it to stay in the `NOTICE` file of anything redistributed from this repository.
6. Define the first deliverable in `docs/DESIGN.md` and plan it in `docs/ROADMAP.md`.
7. Turn on the pre-commit check for private details, once per clone: `git config core.hooksPath .githooks`. See [`docs/PRIVATE_DATA.md`](docs/PRIVATE_DATA.md) for what it catches.
8. Replace the "Using this template" section of `AGENTS.md` with the "Relationship to pz-mod-template" section it provides, and in `CHANGELOG.md` replace the template's history with the mod's own `## [Unreleased]`.
9. Run `bash tools/validate-package.sh`; the remaining warnings list what is still a placeholder.

### Restructure an existing mod

This brings an existing mod's repository into the template's structure: its documentation, repository tooling, and top-level layout. The mod itself does not change, and neither does the existing repository until the last step, when you choose to update it.

**Before you begin**

- The mod must target Build 42. The template's layout, checks, and documents assume it, and the interview stops for a Build 41-only mod.
- The interview needs to read the existing repository: a local folder, or a URL that can be cloned. For a private GitHub repository, run `gh auth login` first.
- Name the new repository whatever suits: the name the mod's repository will finally have, or a temporary one. The last step decides where the result ends up.

**What happens**

Start the interview and answer its first two questions: this is an existing mod, and here is its repository. In Claude Code, `/adopt existing <path or URL>` answers both. With an agent, it does the work below and shows each step; by hand, [`docs/ADOPTION_INTERVIEW.md`](docs/ADOPTION_INTERVIEW.md) gives the same steps with the commands. Then:

1. **Inventory.** The existing repository is read without being changed, and the interview lists what it holds: where the mod package is, the Mod ID and Workshop ID, the current version, the sandbox options, ModData keys, command names, and item types in the source, the documents, the license, and any CI or scripts. You correct the list.
2. **Mapping plan.** It proposes what happens to every file, and copies nothing until you confirm:
   - the mod's package tree is copied exactly as it is, at the same path;
   - `workshop.txt` and `preview.png` are kept exactly, so the Workshop ID carries over and the next upload updates the existing item;
   - the mod's own `LICENSE`, `README.md`, and changelog entries are kept, with the template's Apache license kept beside them for the template material;
   - design notes, to-do lists, test notes, credits, and agent instructions are merged into the template's documents;
   - other scripts and CI workflows are copied as they are, beside the template's;
   - logs, saves, secrets files, archives, and build output are left out.
3. **Copy and check.** The package is copied and compared with the original by Git tree ID; identical IDs mean every file is identical. Then the private-details check, the package validator, and the Lua syntax check run. Nothing inside the package is changed to make them pass: each finding is recorded as a gap in `AGENTS.md` and `docs/ROADMAP.md`, to fix later as an ordinary release. A package that is not at `Contents/mods/<mod-id>/`, for example, fails the validator's layout check until that is done.
4. **Questions.** The same stages as for a new mod, with each answer already filled in from the inventory, so most become "does this still hold?"
5. **Landing.** You choose where the result lives:
   - **Land it back (the default).** The whole restructure becomes one pull request in the existing repository, so its commit history, issues, stars, and the link on the Workshop page all stay. An agent shows the commands, runs them only when you confirm, and checks again that the package is unchanged. The new repository was only a workspace and can be deleted afterward.
   - **Replace.** The new repository becomes the mod's repository, and the old one is archived with a pointer to it. Its history, issues, and pull requests stay behind in the old repository.

**What never changes**

- No file inside the mod's package tree, including `mod.info`, even when a check reports a problem with it.
- The Mod ID, folder names, and every name that saves, server settings, or other mods depend on.
- Anything in the existing repository before the landing step. An agent running the interview never pushes, opens pull requests, or renames, archives, or deletes repositories; it gives you the steps to do those yourself.

## Upgrading a mod created from an earlier template version

`AGENTS.md` in each mod records the template version its files match. Each template release's `Upgrading` notes in [`CHANGELOG.md`](CHANGELOG.md) say whether an existing mod has to do anything; read the notes for every release after the recorded version, apply what fits, and update the recorded version. [How the template is versioned](CHANGELOG.md#how-the-template-is-versioned) explains the version numbers.

## Repository map

### Core — keep from day one

- [`AGENTS.md`](AGENTS.md) — development handoff and working rules. [`CLAUDE.md`](CLAUDE.md) imports it for Claude Code, so every agent reads the same rules.
- [`Contents/mods/`](Contents/mods/) — deployable Project Zomboid mod package.
- [`VERSION`](VERSION), [`CHANGELOG.md`](CHANGELOG.md) — release identity.
- [`LICENSE`](LICENSE), [`NOTICE`](NOTICE) — licensing.
- [`docs/PZ_MODDING_POLICY.md`](docs/PZ_MODDING_POLICY.md), [`CREDITS.md`](CREDITS.md) — modding-policy rules and asset/third-party provenance, which apply from the first commit, not just at release.
- [`docs/PRIVATE_DATA.md`](docs/PRIVATE_DATA.md) — server, player, and credential details that never enter the repository or its GitHub pages, and what to do if one does.
- [`docs/README.md`](docs/README.md), [`docs/DOCUMENTATION_OWNERSHIP.md`](docs/DOCUMENTATION_OWNERSHIP.md) — an index of every document in `docs/`, and which document owns which fact.
- [`docs/DESIGN.md`](docs/DESIGN.md) — requirements, compatibility contracts, and architecture.
- [`docs/ROADMAP.md`](docs/ROADMAP.md) — milestones and current work.
- [`docs/TESTING.md`](docs/TESTING.md) — repeatable test procedure.
- [`docs/VALIDATION_HISTORY.md`](docs/VALIDATION_HISTORY.md) — actual test outcomes.
- [`tools/`](tools/README.md), [`.github/workflows/`](.github/workflows/README.md), [`.githooks/`](.githooks/README.md) — automated checks for the package and version drift, Lua syntax, and private details, run locally, in CI, and (once turned on) before each commit. Each link opens that folder's README.

### Add when needed

- [`docs/adr/`](docs/adr/README.md) — durable decision records, once a decision has real alternatives.
- [`docs/spikes/`](docs/spikes/README.md) — bounded feasibility investigations, once engine behavior needs an experiment.
- [`docs/RELEASING.md`](docs/RELEASING.md), [`workshop.txt`](workshop.txt), [`docs/workshop-description.bbcode`](docs/workshop-description.bbcode) — release checklist, Workshop publication, and rollback. Add `preview.png` at the root before the first upload; remove the Workshop files if not publishing there.

### Optional — delete freely if you don't use the workflow

- [`docs/ADOPTION_INTERVIEW.md`](docs/ADOPTION_INTERVIEW.md), [`.claude/`](.claude/README.md) — the setup questions, for a new mod or an existing one, and the `/adopt` command that asks them in Claude Code; delete both once the mod is set up. Delete `.claude/` and `CLAUDE.md` if the mod does not use Claude Code.
- [`docs/RESEARCH_LINKS.md`](docs/RESEARCH_LINKS.md) — external reference links and mods studied for ideas.
- [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE/), [`.github/pull_request_template.md`](.github/pull_request_template.md), [`.github/FUNDING.yml`](.github/FUNDING.yml) — Project Zomboid-specific issue templates, the questions each pull request answers, and optional sponsor links; the funding file is all comments until filled in.

Test logs, decompiled game source, and research material stay in local folders outside the repository; [`docs/TESTING.md`](docs/TESTING.md#local-files-and-automation) explains how to give a coding agent access to them and what test-cycle scripts are worth adding to `tools/`.

## License and status

The template's original material is Copyright 2026 Jonathan Jacobs and licensed under Apache-2.0; see [`NOTICE`](NOTICE). Project Zomboid code and assets remain property of their respective owners and are neither redistributed nor relicensed here. A project created from this template is an unofficial independent community mod unless documented otherwise.
