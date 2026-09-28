# Validation history

Status: **No validation has been recorded.**

Record only tests that actually occurred, including observations from normal play. Do not place planned tests here; use [`TESTING.md`](TESTING.md) or [`ROADMAP.md`](ROADMAP.md).

This is an append-only ledger. If a later run overturns an earlier entry, add a new dated entry that says so — correcting or withdrawing the earlier finding — rather than editing history.

| Date | Version | Scope | Outcome | Evidence |
| --- | --- | --- | --- | --- |
| `TBD` | `TBD` | `TBD` | `TBD` | `TBD` |

The table is an index. When an entry needs more than a line, add a dated section below it in this shape:

```markdown
## <YYYY-MM-DD> — <what was tested>

Build `<x.y.z>` on Project Zomboid `<version>` `<revision>`; <topology: single-player, hosted, or dedicated, and player count>. Logs reviewed: <which, from what window>.

- <what was observed, with the relevant log values>
- <…>

Result: <PASS / FAIL / PASS with conditions> for <which checks in TESTING.md>.

Not covered: <what did not happen during the window or was not reviewed, so no one later reads this entry as proving it>.
```

For a Project Zomboid update, this entry is the compatibility checkpoint: record it before changing any "tested with" claim or `versionMin=`.
