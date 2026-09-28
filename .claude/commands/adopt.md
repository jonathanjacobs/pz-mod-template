---
description: Set up a new mod, or restructure an existing mod's repository, by asking the adoption interview one stage at a time
argument-hint: "[new | existing <path or URL> | stage <N or E1-E3>]  (optional)"
---

Run the adoption interview in `docs/ADOPTION_INTERVIEW.md` with the user, and write their answers into the files it names.

Optional argument: `$ARGUMENTS`. `new` answers stage 0 with a new mod. `existing` followed by a folder path or URL answers stage 0 with an existing mod at that location. `stage N` (or `stage E1` to `stage E3`) runs only that stage. When the argument is empty, start at stage 0.

## Before you start

Run `git remote get-url origin`. If it points at `jonathanjacobs/pz-mod-template`, stop: this is the template itself, and the interview would rewrite it. Tell the user to create their own repository with "Use this template" first, as "Before you start" in the interview describes.

Read `docs/ADOPTION_INTERVIEW.md`, `AGENTS.md`, and `README.md`. The interview document is the only source of questions. Do not add questions, and do not ask for anything a file already answers; show the existing answer and ask whether it still holds.

## How to run it

Ask one stage at a time. Present that stage's questions, then stop and wait. Do not move to the next stage, and do not write any file, until the user has answered the stage in front of them.

After stage 1, say which stages apply and which are skipped, with the reason from the stage 1 table, and confirm that list before going on.

Never supply an answer the user did not give. When they do not know, ask whether the question applies, then write `not applicable` or `TBD` and say which you wrote. Accept a partial answer and move on.

## Writing the answers

Before writing, show the text you propose and the file it goes into. Make each stage one self-contained change, so the user can stop after any stage and leave the repository consistent. Use the user's own words for what the mod does wherever they gave a usable sentence.

Follow `AGENTS.md` in everything you write: American English, no hard-wrapped markdown, and no private details. Stage 8 asks about player names and server host names; if the user types one anyway, do not repeat it or write it anywhere, and point them to adding it as a pattern themselves as `docs/PRIVATE_DATA.md` describes.

For a new mod, stage 2 renames `Contents/mods/pz-mod-id/` with `git mv` and keeps `VERSION`, both `modversion=` lines, and any version in `workshop.txt` equal. Run `bash tools/validate-package.sh` after the stage and report its errors and warnings as they are.

Do not record that the mod is tested, compatible with a build, or ready for release. The interview produces no evidence of any of those.

## An existing mod

Follow the ground rules in the interview without exception:

- The existing repository is read only. For a URL, clone it into a temporary folder outside the new repository; for a local folder, read it in place, and ask the user to run `/add-dir <path>` if access is refused. Never write to it before stage 10.
- Nothing inside the mod's package tree changes. Copy it byte for byte at its existing path. Do not reformat, rename, re-encode, or "fix" any file in it, including `mod.info`, even when the validator reports an error there; record the error as a gap instead.
- Never rename the Mod ID, a mod folder, a sandbox option, a ModData key, a command name, a script module, or a Lua file.

In E1, show the inventory and ask the user to correct it. If the mod targets only Build 41, say so and stop. In E2, show the complete mapping plan and wait for confirmation before copying anything. In E3, commit the unchanged copies separately from the merges when the user agrees, and confirm the package tree is identical to the original, by comparing tree IDs as step 2 of E3 describes, before going on. Show both IDs. Report every finding of `check-sensitive-content.sh`, `validate-package.sh`, and `check-lua-syntax.sh` as it is.

In stages 1 to 9, pre-fill each answer from what E1 found, say where it came from, and ask whether it holds. In stage 4, list every contract found in the source.

In stage 10, explain both choices and let the user pick. For "land it back", show the commands with the real paths filled in and run them only when the user confirms, then show the result of the package-tree check. Never push, open a pull request, rename, archive, or delete a repository; give the user the commands or steps to do it themselves.

## Finishing

Run stage 9 after stages 1 to 8, and stage 10 last for an existing mod. In stage 9, list what appears unused and delete only what the user confirms; never delete anything copied from an existing repository.

End by listing the stages answered, the stages skipped and why, every `TBD` left with the file it is in, and for an existing mod every recorded gap. Say that `validate-package.sh` warnings name what is still a placeholder. Do not commit unless the user asks.
