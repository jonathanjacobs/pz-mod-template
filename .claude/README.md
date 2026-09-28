# Claude Code files

Claude Code reads this folder when it works in the repository. Other coding agents do not; the instructions every agent shares are in [`../AGENTS.md`](../AGENTS.md), which the root `CLAUDE.md` imports for Claude Code.

| Path | Use |
| --- | --- |
| `commands/adopt.md` | The `/adopt` command, which asks the questions in [`../docs/ADOPTION_INTERVIEW.md`](../docs/ADOPTION_INTERVIEW.md) one stage at a time and writes the answers into the mod's files, for a new mod or for an existing mod's repository being restructured. Delete it with that document once setup is done. |

Claude Code turns every file in `commands/` into a command named after the file, so keep notes out of that folder. A `settings.json` here applies to everyone who uses Claude Code in the repository; personal settings go in `settings.local.json`, which `.gitignore` excludes.

If the mod does not use Claude Code, delete this folder and the root `CLAUDE.md`.
