---
description: Set up a new mod, or restructure an existing mod's repository, by asking the adoption interview one stage at a time
argument-hint: "[new | existing <path or URL> | stage <N or E1-E3>]  (optional)"
---

Run the adoption interview in `docs/ADOPTION_INTERVIEW.md` with the user, and write their answers into the files it names. Follow its section "Running this interview with an agent" exactly; it holds every rule for asking, writing, handling an existing repository, and landing the result. Read that section before doing anything else, including its check that this repository is not the template itself.

Optional argument: `$ARGUMENTS`. `new` answers stage 0 with a new mod. `existing` followed by a folder path or URL answers stage 0 with an existing mod at that location. `stage N` (or `stage E1` to `stage E3`) runs only that stage. When the argument is empty, start at stage 0.
