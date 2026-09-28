# Adoption interview

Do not update for: one mod's answers, which go into the files each stage names.

This document sets up a mod from the template as a series of questions, asked in order, with the file each answer goes into. It covers both a new mod and an existing mod whose repository is being restructured to match the template. Work through it alone, or run `/adopt` in Claude Code to have an agent ask the questions one stage at a time and write the answers in. The README's "Start a new mod, or restructure an existing one" list is the same setup for a new mod as a checklist; this document adds the questions behind each step and says which steps a given mod can skip.

Every mod starts at stage 0. A new, small, single-player mod then needs stages 1 to 4, 8, and 9, which take about twenty minutes. An existing mod also goes through stages E1 to E3 before stage 1, and stage 10 at the end.

Two answers are always acceptable: `TBD`, meaning the question applies and nobody has decided yet, and `not applicable`, meaning it was asked and does not apply to this mod. Write whichever is true; an honest `TBD` is more useful than a guess.

## Before you start

1. On GitHub, open [pz-mod-template](https://github.com/jonathanjacobs/pz-mod-template) and choose **Use this template → Create a new repository**. This gives a repository of your own with none of the template's history. For an existing mod, name it whatever suits: the name the mod's repository will finally have, or a temporary name. Stage 10 decides where the finished result ends up.
2. Clone the new repository, open it in Claude Code, and run `/adopt`. Without Claude Code, work through the stages below by hand.

Do not run the interview in a clone of pz-mod-template itself; it rewrites the template's files.

## Stage 0 — Starting point

1. **Are you creating a new mod from scratch, or restructuring an existing mod's repository to match the template?**
2. **For an existing mod: where is its repository?** A local folder, or a URL on GitHub or another Git host.

A new mod goes on to [stage 1](#stage-1--scope). An existing mod goes on to [stage E1](#stage-e1--read-the-existing-repository), after reading the ground rules below.

## Restructuring an existing mod

### Ground rules

- **Nothing inside the mod's package tree changes.** Every Lua file, script, translation, `mod.info`, sandbox-options file, and asset is copied byte for byte, at the path it has now. The Mod ID, folder names, and every [compatibility contract](DESIGN.md#compatibility-contracts) stay exactly as they are.
- **Adoption changes documentation, repository tooling, and top-level layout only.** Where the template would do something differently inside the package, such as its folder layout, a `mod.info` field, or the build stamp, record it as a gap and leave it for a later change with its own test.
- **The existing repository is only read.** Nothing is written to it until stage 10, and only if you choose to land the result there.

### Stage E1 — Read the existing repository

A local folder is read in place; Claude Code asks permission before reading outside the new repository, or `/add-dir <path>` grants it for the session. A URL is cloned into a temporary folder outside the new repository. A private repository needs `gh auth login` first.

Record what is there, without changing anything:

- **Package:** where each mod folder is, how many mods the repository holds, each Mod ID, the `mod.info` keys in use (`modversion=` or the older `version=`), and which builds it targets (a `42/` folder, a `common/` folder, or a Build 41 layout).
- **Workshop:** whether `workshop.txt` exists and has an `id=`, and which of `preview.png`, poster, and icon exist.
- **Version:** the current version, and every place it is stated: `mod.info`, tags, changelog, README, Workshop text.
- **Compatibility contracts in the source:** sandbox options (`option <Prefix>.<Name>` in `sandbox-options.txt`), ModData keys, client/server command module names, script modules (`module <Name> {` in `media/scripts/`), and shared Lua modules other mods may `require`.
- **Documents:** README, changelog, design notes, to-do lists, test notes, credits, agent instructions (`AGENTS.md`, `CLAUDE.md`, or others), and where each lives.
- **License:** which one, or none.
- **Tooling:** CI workflows, build or deploy scripts, `.gitignore`, `.gitattributes`.
- **Never to be copied:** logs, saves, `.env` or other secrets files, archives, build output, decompiled source.

If the mod targets only Build 41, stop here and say so: the template's layout, validator, and documents assume Build 42.

**Answers go in:** nothing yet. Show the inventory and correct it together.

### Stage E2 — Plan the mapping

Decide, for every file and folder found in E1, one of: **copy as is** (same path, same bytes), **merge** into a template file, **replace** a template file, or **leave out** with a reason. The defaults:

| In the existing repository | Plan |
| --- | --- |
| The mod's package tree, wherever it is | Copy as is, at its existing path, and delete the template's placeholder `Contents/mods/pz-mod-id/` |
| `workshop.txt`, `preview.png` | Copy as is, replacing the template's. The `id=` line must survive exactly, or the next upload creates a new Workshop item |
| `LICENSE` | Keep the mod's own as `LICENSE`. Keep the template's Apache 2.0 text beside it as `LICENSE-pz-mod-template`, which covers the template material. If the mod has no license, ask the owner which to use; do not leave the template's `LICENSE` in place as if it covered the mod unless they choose Apache 2.0 |
| `README.md` | Keep the mod's as the root README, replacing the template's. Add any sections the template suggests only if the owner wants them |
| Changelog | Keep the mod's entries under the template's format paragraph, and drop the template's own history |
| Design notes, to-do lists, test notes | Merge into `DESIGN.md`, `ROADMAP.md`, and `TESTING.md`. Only tests that actually happened go into `VALIDATION_HISTORY.md` |
| `AGENTS.md`, `CLAUDE.md`, other agent instructions | Merge the mod's rules into the template's `AGENTS.md`. `CLAUDE.md` keeps its `@AGENTS.md` line plus any Claude-only notes |
| Credits or attribution files | Merge into `CREDITS.md` |
| CI workflows, other scripts and tools | Copy as is at their existing paths, beside the template's |
| `.gitignore`, `.gitattributes` | Merge |
| Logs, saves, secrets files, archives, build output, decompiled source | Leave out |

**Answers go in:** nothing yet. Show the full plan and confirm it before anything is copied.

### Stage E3 — Copy and check

1. Copy the "copy as is" and "replace" items first, and commit them on their own, so the unchanged files form one commit that is easy to verify. From a Git repository, `git -C <existing> archive HEAD <paths> | tar -x` copies tracked files only, which keeps stray local files out.
2. Confirm the package tree is identical to the original. `git -C <existing> rev-parse HEAD:<package-path>` and `git rev-parse HEAD:<package-path>` must print the same ID; Git gives two trees the same ID only when every file in them is identical. When the existing mod is a plain folder without Git, use `git diff --no-index --stat <existing>/<package-path> <package-path>`, which prints nothing when the files match but can overlook line-ending differences.
3. Make the merges from the plan, as a second commit.
4. Run `bash tools/check-sensitive-content.sh` over the whole repository. Anything it finds in copied files is also in the existing repository's history; follow [`PRIVATE_DATA.md`](PRIVATE_DATA.md#if-private-details-reach-github).
5. Run `bash tools/validate-package.sh` and `bash tools/check-lua-syntax.sh`. Do not fix anything inside the package to make them pass; record each error as a gap. If the package is not at `Contents/mods/<mod-id>/`, the validator stops at its layout check. Either leave the `Validate Package` workflow failing as a visible reminder, or turn off its `validate-package` job until the layout is changed in a later release.

**Answers go in:** each gap as a line in "Current development context" in `AGENTS.md`, and as a task in [`ROADMAP.md`](ROADMAP.md).

Then continue with stage 1. For an existing mod, each stage starts from what E1 found: show the answer and where it came from, and ask whether it still holds.

## Stage 1 — Scope

1. **Where will the mod run?** Single-player only · multiplayer only · both.
2. **Will it be published on the Steam Workshop?** Yes · not yet decided · no.
3. **Will it distribute any non-code files** (poster, icon, textures, sounds, models), **or anything not written from scratch for this mod,** such as code or data from another mod, or images made with a generation tool? Yes · no.
4. **How will it be tested?** On this machine only · also on a dedicated server reached remotely.

Stages 2, 3, 4, 8, and 9 apply to every mod. The answers switch on the rest:

| If you answered | Then this also applies |
| --- | --- |
| Question 1: multiplayer only, or both | Stage 5 |
| Question 2: yes, or not yet decided | Stage 6 |
| Question 2: yes | Stage 7, for the Workshop artwork |
| Question 3: yes | Stage 7 |
| Question 4: a remote dedicated server | The remote-server part of stage 8 |

The answer to question 2 also decides what stage 9 removes.

## Stage 2 — Identity

- What is the mod's name, as players will see it?
- What is its Mod ID? Keep it short, with no spaces. It can never change after the first public release, because servers and saved worlds refer to the mod by it.
- What author name should `mod.info` carry? Use a public modding name.
- Which Project Zomboid build is the target, and which is the oldest build it will be tested on (`versionMin=`)?
- Which version does the mod start at? `0.1.0` is usual.
- Does it already have a Steam Workshop ID?

**Answers go in:** the renamed folder `Contents/mods/<mod-id>/`; both `mod.info` files; `VERSION`; the "Project facts" in `AGENTS.md`; the first line of `NOTICE`, above the pz-mod-template block; and `workshop.txt`. Keep `VERSION`, `modversion=`, and any `vX.Y.Z` in `workshop.txt` equal, then run `bash tools/validate-package.sh`.

**For an existing mod:** nothing is renamed and `mod.info` is not edited. Set `VERSION` to the mod's current version, and fill in the "Project facts" and `NOTICE`.

## Stage 3 — What the mod does

- In one or two sentences, what does the mod do, and for whom: players, server operators, or both?
- What is deliberately outside it?
- Finish this sentence three to five times: *The mod is working when ___.* For each, how would you see it: in game, in a log line, or in a setting?
- What is the first milestone: the smallest version worth playing? For an existing mod, what is the next one?

**Answers go in:** Scope and Behavior (`R1`, `R2`, …) under Requirements in [`DESIGN.md`](DESIGN.md), and the current milestone in [`ROADMAP.md`](ROADMAP.md). A small mod can answer this whole stage in a few lines.

## Stage 4 — Compatibility contracts

These names are stored in saves and server settings or used by other mods, so they are hard to change later. Name what is planned; `TBD` is fine for what is not yet decided. For an existing mod, confirm the names E1 found in the source, and list them all: every one is already in use.

- Will the mod add sandbox options? Under which prefix (`option <Prefix>.<Name>` in `sandbox-options.txt`)?
- Will it store data in ModData on players, the world, or objects? Under which key?
- Will clients and the server send each other commands? Under which module name?
- Will it add items, recipes, or other scripts? Under which script module?
- Should other mods be able to build on it by requiring its Lua modules?

**Answers go in:** the Compatibility contracts table in [`DESIGN.md`](DESIGN.md#compatibility-contracts), starting with the Mod ID row.

## Stage 5 — Multiplayer

- Which state must the server own, so that a client can never decide it alone?
- Is the main target a dedicated server, a hosted game, or both?
- What prefix will the mod's log lines use, such as `[ModName]`?
- Where will the shared version module live (the build stamp in [`DESIGN.md`](DESIGN.md#build-stamp-and-version-handshake))? For an existing mod without one, record adding it as a gap.

**Answers go in:** "Primary supported mode" and Behavior in [`DESIGN.md`](DESIGN.md), "Primary multiplayer target" in `AGENTS.md`, and the log prefix in "Chasing a problem" in [`TESTING.md`](TESTING.md). For a single-player-only mod, record that in `DESIGN.md` and delete the build-stamp section.

## Stage 6 — Workshop publication

- What are the public title, the one-line summary, and the tags (for example `Build 42`, `Multiplayer`)?
- Stay `private` until the first public release?
- Who will make the preview image, poster, and icon, and how: drawn, photographed, or generated with a named tool?
- Will the description have a support or donation section? Donations may unlock nothing (rule 6 in [`PZ_MODDING_POLICY.md`](PZ_MODDING_POLICY.md)).

For an existing Workshop item, paste the current Steam description into `workshop-description.bbcode`, so the repository holds the text that is live now.

**Answers go in:** `workshop.txt`, [`workshop-description.bbcode`](workshop-description.bbcode), and the Mod ID and Workshop ID lines at the top of [`RELEASING.md`](RELEASING.md). The artwork's origin goes in stage 7.

## Stage 7 — Assets and outside material

For each distributed non-code file, and each piece of code, data, or art from outside the mod:

- What is it, and where did it come from: original, generated with a named tool, or third-party?
- Who made it?
- On what basis may the mod distribute it: original work, a license (which one), or written permission?
- Was it modified, and does its license require attribution or other conditions?

Write `unresolved` where you cannot answer, and do not ship that item until the answer is known. Mods studied only for ideas are not distributed; list them separately.

**Answers go in:** [`../CREDITS.md`](../CREDITS.md), and mods studied for ideas in [`RESEARCH_LINKS.md`](RESEARCH_LINKS.md).

## Stage 8 — Testing and private details

- Where will tests run: single-player, a hosted game, a local dedicated server, or a remote one? How many players can join a multiplayer test?
- What is the simplest sign in game that the mod is working? This becomes step 2 of the smoke test.
- Turn on the pre-commit check now: `git config core.hooksPath .githooks`.
- Are there player names or server host names that must never appear in the repository? Do not type them into this interview. Add them yourself, as described in [`PRIVATE_DATA.md`](PRIVATE_DATA.md#automated-check): in a `SENSITIVE_PATTERNS` repository secret, and in a patterns file outside the repository.
- Where will test logs, and any decompiled source or research material, be kept? Use local folders outside the repository, and grant a coding agent access to them as [Local files and automation](TESTING.md#local-files-and-automation) describes.
- For a remote server: create `.env.server` from the placeholder layout in that same section, and fill it in locally. It stays out of Git.

**Answers go in:** "Before testing" and "Smoke test" in [`TESTING.md`](TESTING.md), and [`../tools/README.md`](../tools/README.md) when test-cycle scripts are added.

## Stage 9 — Removing what you do not use

- Delete what stage 1 ruled out:
  - not publishing on the Workshop: `workshop.txt`, `docs/workshop-description.bbcode`, and the Workshop sections of `RELEASING.md`;
  - no issue tracker or sponsor links: `.github/ISSUE_TEMPLATE/` and `.github/FUNDING.yml`.
- For an existing mod, delete only template files; never delete anything copied from the existing repository.
- Replace the "Using this template" section of `AGENTS.md` with the "Relationship to pz-mod-template" section it provides.
- In `CHANGELOG.md`, delete "How the template is versioned" and the template's entries. A new mod starts its own history with `## [Unreleased]`; an existing mod keeps its own entries and adds one under `## [Unreleased]` saying the repository was restructured to pz-mod-template and at which version.
- A new mod replaces `README.md` with its own, using the sections suggested in the template README's step 4.
- Delete this document and `.claude/commands/adopt.md` once setup is done, and remove their mentions from `AGENTS.md`, the root `README.md`, this folder's index in [`README.md`](README.md), and [`DOCUMENTATION_OWNERSHIP.md`](DOCUMENTATION_OWNERSHIP.md). Template upgrades later come from the template's `CHANGELOG.md`, not from this document.
- Run `bash tools/validate-package.sh`; each remaining warning names something still a placeholder, and for an existing mod, each error should already be a recorded gap.

A mod that deletes half the optional folders on its first day has used the template as intended.

## Stage 10 — Landing the result (existing mods only)

Choose where the restructured repository lives from now on.

**Land it back (the default).** The result becomes one pull request in the existing repository, which keeps its commit history, issues, pull requests, stars, and every link to it, including the one on the Workshop page. The new repository was only a workspace and can be deleted afterward. In an up-to-date clone of the existing repository, with no uncommitted changes:

```bash
git switch -c adopt-pz-mod-template
git rm -rq .
git -C <new-repository> archive HEAD | tar -x
git add -A
```

`git rm -rq .` removes only tracked files, so ignored local files stay where they are. Before committing, check that the package tree did not change: `git diff --cached --stat -- <package-path>` must print nothing. A change there usually means line endings differ between the two repositories; find the cause before going on. Then commit, and confirm `git rev-parse HEAD:<package-path>` prints the same ID as it did on the existing repository's default branch. Push the branch and open the pull request.

**Replace.** The new repository becomes the mod's repository. The old one loses its place as the mod's home, and its history, issues, and pull requests stay behind in it. Archive the old repository on GitHub with a note pointing to the new one, and update every link to it: the Workshop description, the README, and any `url=` in `mod.info` (in a later release, since `mod.info` is inside the package). To give the new repository the old name, rename the old one first.

**Answers go in:** the `CHANGELOG.md` entry from stage 9, which says which way the result landed.
