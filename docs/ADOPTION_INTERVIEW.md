# Adoption interview

Do not update for: one mod's answers, which go into the files each stage names.

This document sets up a mod from the template as a series of questions, asked in order, with the file each answer goes into. Work through it alone, or run `/adopt` in Claude Code to have an agent ask the questions one stage at a time and write the answers in. It also covers bringing an existing mod closer to the template, one gap at a time. The README's "Start a new mod" list is the same setup as a checklist; this document adds the questions behind each step and says which steps a given mod can skip.

Stage 1 decides which later stages apply. A small single-player mod needs stages 1 to 4, 8, and 9, and takes about twenty minutes.

Two answers are always acceptable: `TBD`, meaning the question applies and nobody has decided yet, and `not applicable`, meaning it was asked and does not apply to this mod. Write whichever is true; an honest `TBD` is more useful than a guess.

## Which path are you on

- **A new mod created from this template:** work through the stages in order.
- **An existing mod,** with its own code or an item already on the Workshop: start at [Existing mods](#existing-mods), which changes nothing until you have chosen one gap to work on.

## Stage 1 — Scope

1. **Where will the mod run?** Single-player only · multiplayer only · both.
2. **Will it be published on the Steam Workshop?** Yes · not yet decided · no.
3. **Will it distribute any non-code files** (poster, icon, textures, sounds, models), **or anything not written from scratch for this mod,** such as code or data from another mod, or images made with a generation tool? Yes · no.
4. **How will it be tested?** On this machine only · also on a dedicated server reached remotely.
5. **Will you keep decompiled game source, saved documentation, or other mods on this machine for study?** Yes · no.

Stages 2, 3, 4, 8, and 9 apply to every mod. The answers switch on the rest:

| If you answered | Then this also applies |
| --- | --- |
| Question 1: multiplayer only, or both | Stage 5 |
| Question 2: yes, or not yet decided | Stage 6 |
| Question 2: yes | Stage 7, for the Workshop artwork |
| Question 3: yes | Stage 7 |
| Question 4: a remote dedicated server | The remote-server part of stage 8 |

Answers to questions 2, 4, and 5 also decide what stage 9 removes.

## Stage 2 — Identity

- What is the mod's name, as players will see it?
- What is its Mod ID? Keep it short, with no spaces. It can never change after the first public release, because servers and saved worlds refer to the mod by it.
- What author name should `mod.info` carry? Use a public modding name.
- Which Project Zomboid build is the target, and which is the oldest build it will be tested on (`versionMin=`)?
- Which version does the mod start at? `0.1.0` is usual.
- Does it already have a Steam Workshop ID?

**Answers go in:** the renamed folder `Contents/mods/<mod-id>/`; both `mod.info` files; `VERSION`; the "Project facts" in `AGENTS.md`; the first line of `NOTICE`, above the pz-mod-template block; and `workshop.txt`. Keep `VERSION`, `modversion=`, and any `vX.Y.Z` in `workshop.txt` equal, then run `bash tools/validate-package.sh`.

## Stage 3 — What the mod does

- In one or two sentences, what does the mod do, and for whom: players, server operators, or both?
- What is deliberately outside it?
- Finish this sentence three to five times: *The mod is working when ___.* For each, how would you see it: in game, in a log line, or in a setting?
- What is the first milestone: the smallest version worth playing?

**Answers go in:** Scope and Behavior (`R1`, `R2`, …) under Requirements in [`DESIGN.md`](DESIGN.md), and the current milestone in [`ROADMAP.md`](ROADMAP.md). A small mod can answer this whole stage in a few lines.

## Stage 4 — Compatibility contracts

These names are stored in saves and server settings or used by other mods, so they are hard to change later. Name what is planned; `TBD` is fine for what is not yet decided.

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
- Where will the shared version module live (the build stamp in [`DESIGN.md`](DESIGN.md#build-stamp-and-version-handshake))?

**Answers go in:** "Primary supported mode" and Behavior in [`DESIGN.md`](DESIGN.md), "Primary multiplayer target" in `AGENTS.md`, and the log prefix in "Chasing a problem" in [`TESTING.md`](TESTING.md). For a single-player-only mod, record that in `DESIGN.md` and delete the build-stamp section.

## Stage 6 — Workshop publication

- What are the public title, the one-line summary, and the tags (for example `Build 42`, `Multiplayer`)?
- Stay `private` until the first public release?
- Who will make the preview image, poster, and icon, and how: drawn, photographed, or generated with a named tool?
- Will the description have a support or donation section? Donations may unlock nothing (rule 6 in [`PZ_MODDING_POLICY.md`](PZ_MODDING_POLICY.md)).

**Answers go in:** `workshop.txt`, `workshop-description.bbcode`, and the Mod ID and Workshop ID lines at the top of [`RELEASING.md`](RELEASING.md). The artwork's origin goes in stage 7.

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
- For a remote server: copy `scripts/server.env.example` to `.env.server` and fill it in locally. It stays out of Git.

**Answers go in:** "Before testing" and "Smoke test" in [`TESTING.md`](TESTING.md), and [`../scripts/README.md`](../scripts/README.md) when scripts are added.

## Stage 9 — Removing what you do not use

- Delete what stage 1 ruled out:
  - not publishing on the Workshop: `workshop.txt`, `workshop-description.bbcode`, and the Workshop sections of `RELEASING.md`;
  - testing on this machine only, with no plans for scripts: `scripts/`;
  - no decompiled source or research material: `decompiled/` and `research-source/`, with their `.gitignore` entries;
  - no issue tracker or sponsor links: `.github/ISSUE_TEMPLATE/` and `.github/FUNDING.yml`.
- Replace the "Using this template" section of `AGENTS.md` with the "Relationship to pz-mod-template" section it provides.
- In `CHANGELOG.md`, delete "How the template is versioned" and the template's entries, and start the mod's own history with `## [Unreleased]`.
- Replace `README.md` with the mod's own, using the sections suggested in the template README's step 4.
- Delete this document and `.claude/commands/adopt.md` once setup is done, and remove their mentions from `AGENTS.md`, `README.md`, and [`DOCUMENTATION_OWNERSHIP.md`](DOCUMENTATION_OWNERSHIP.md). Template upgrades later come from the template's `CHANGELOG.md`, not from this document.
- Run `bash tools/validate-package.sh`; each remaining warning names something still a placeholder.

A mod that deletes half the optional folders on its first day has used the template as intended.

## Existing mods

Fill in this table before changing any file. It records what the repository already answers, and where.

| Question the template asks | Where this repository already answers it | Good enough for now? |
| --- | --- | --- |
| What does the mod do, and how is it installed and configured? | | |
| What must it do (requirements)? | | |
| Which names do saves, server settings, or other mods depend on? | | |
| How is it tested, and what has been observed? | | |
| How is a release made, published, and rolled back? | | |
| Where did every distributed asset come from? | | |
| What keeps private details out of the repository? | | |
| Does `bash tools/validate-package.sh` pass on the package? | | |

Then work one gap at a time:

1. Pick one row, choosing the gap that has already cost time or caused a problem.
2. Run the one stage that answers it, and no others.
3. Improve or link the document that already answers the question. Create a file with the template's name only when nothing in the repository answers it.
4. Never rename the Mod ID, the mod folder, sandbox options, ModData keys, or Lua files to match the template: each is a compatibility contract that published copies depend on. A change to the package layout, such as adding the Build 42 `common/` folder, is its own task with its own test.
5. Before turning on the sensitive-content workflow, run `bash tools/check-sensitive-content.sh` over the whole repository. Anything it finds that is already pushed stays in Git history; follow [`PRIVATE_DATA.md`](PRIVATE_DATA.md#if-private-details-reach-github).
6. Record the template version the adopted files came from in the "Project facts" of `AGENTS.md`.

Come back when the next gap starts to cost time.
