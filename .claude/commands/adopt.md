---
description: Set up this mod from the template by asking the adoption interview one stage at a time
argument-hint: "[new | existing | stage N]  (optional)"
---

Run the adoption interview in `docs/ADOPTION_INTERVIEW.md` with the user, and write their answers into the files it names.

Optional argument: `$ARGUMENTS`. Treat `new` or `existing` as the path to take, and `stage N` as a request to run only that stage. When it is empty, decide the path from the repository and say which one you chose and why. A repository is an existing mod when it has its own Lua code, a Workshop ID in `workshop.txt`, or a README written for a real mod. Otherwise it is new.

## Before you start

Read `docs/ADOPTION_INTERVIEW.md`, `AGENTS.md`, and `README.md`. The interview document is the only source of questions. Do not add questions, and do not ask for anything a file already answers; show the existing answer and ask whether it still holds.

## How to run it

Ask one stage at a time. Present that stage's questions, then stop and wait. Do not move to the next stage, and do not write any file, until the user has answered the stage in front of them.

After stage 1, say which stages apply and which are skipped, with the reason from the stage 1 table, and confirm that list before going on.

Never supply an answer the user did not give. When they do not know, ask whether the question applies, then write `not applicable` or `TBD` and say which you wrote. Accept a partial answer and move on.

## Writing the answers

Before writing, show the text you propose and the file it goes into. Make each stage one self-contained change, so the user can stop after any stage and leave the repository consistent. Use the user's own words for what the mod does wherever they gave a usable sentence.

Follow `AGENTS.md` in everything you write: American English, no hard-wrapped markdown, and no private details. Stage 8 asks about player names and server host names; if the user types one anyway, do not repeat it or write it anywhere, and point them to adding it as a pattern themselves as `docs/PRIVATE_DATA.md` describes.

In stage 2, rename `Contents/mods/pz-mod-id/` with `git mv`, and keep `VERSION`, both `modversion=` lines, and any version in `workshop.txt` equal. Run `bash tools/validate-package.sh` after the stage and report its errors and warnings as they are.

Do not record that the mod is tested, compatible with a build, or ready for release. The interview produces no evidence of any of those.

## An existing mod

Fill in the gap-scan table from `docs/ADOPTION_INTERVIEW.md` first, by reading the repository, and change no files while you do. Show the table and ask the user to correct it. Then ask which single gap to work on and run only the stage that answers it. Never rename the Mod ID, the mod folder, sandbox options, ModData keys, or Lua files to match the template.

## Finishing

Run stage 9 last. List what appears unused and delete only what the user confirms.

End by listing the stages answered, the stages skipped and why, and every `TBD` left with the file it is in. Say that `validate-package.sh` warnings name what is still a placeholder. Do not commit unless the user asks.
