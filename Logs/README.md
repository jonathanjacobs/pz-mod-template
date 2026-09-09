# Local test logs (not committed)

This folder is gitignored (`Logs/` in `.gitignore`). Drop raw client/server logs from each test session here; they are analysis input, not repository content. Remove this folder and its `.gitignore` entry if the project does not need it.

## Suggested convention

No subfolders. After each test, drop two archives directly here: one client, one server, each containing that side's log output. The most recent client/server pair (by file modified time) corresponds to the most recent test; timestamps inside the logs resolve any ambiguity. Older archives can accumulate or be deleted as convenient — this folder is never committed either way.

Findings distilled from these logs belong in `docs/VALIDATION_HISTORY.md` or a `docs/spikes/` entry, per `docs/DOCUMENTATION_OWNERSHIP.md`. The raw logs themselves are never committed.
