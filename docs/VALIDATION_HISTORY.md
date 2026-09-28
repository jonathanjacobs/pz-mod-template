# Validation history

Status: **No validation has been recorded.**

Do not update for: planned tests ([`TESTING.md`](TESTING.md) or [`ROADMAP.md`](ROADMAP.md)), or correcting an earlier entry in place (add a new entry instead).

Record only tests that actually occurred, including observations from normal play.

This is an append-only ledger. If a later run overturns an earlier entry, add a new dated entry that says so — correcting or withdrawing the earlier finding — rather than editing history.

| Date | Version | Scope | Outcome | Evidence |
| --- | --- | --- | --- | --- |
| `TBD` | `TBD` | `TBD` | `TBD` | `TBD` |

The table is an index. When an entry needs more than a line, add a dated section below it in this shape:

```markdown
## <YYYY-MM-DD> — <what was tested>

Build `<x.y.z>` on Project Zomboid `<version>` `<revision>`; <topology: single-player, hosted, or dedicated, and player count, described by kind>. Logs reviewed: <which, from what window>.

- <what was observed, with the relevant log values>
- <…>

Result: <one result per check in TESTING.md, for example "smoke test PASS; core behavior INCOMPLETE">.

Not covered: <what did not happen during the window or was not reviewed, so no one later reads this entry as proving it>.
```

## Results

Give each check one of these results, in the index table and in the entry:

| Result | Meaning |
| --- | --- |
| `PASS` | Everything the check covers was observed and behaved as expected |
| `PASS with conditions` | It behaved as expected only within stated limits, such as one topology or with an option off; the entry says which |
| `FAIL` | Something the check covers behaved wrongly; link the issue |
| `INCOMPLETE` | The check started but not everything it covers was observed, for example because the session ended early or the situation never came up |
| `NOT RUN` | The check was part of this session's plan but was not performed |

Only `PASS` and `PASS with conditions` count as evidence for the [release checklist](RELEASING.md#release-checklist). `INCOMPLETE` and `NOT RUN` are recorded so a gap stays visible; they are not partial passes.

Entries are public. Describe servers by kind ("a rented dedicated server"), and replace IP addresses, Steam IDs, and other players' names in quoted log values with placeholders; see [`PRIVATE_DATA.md`](PRIVATE_DATA.md).

For a Project Zomboid update, this entry is the compatibility checkpoint: record it before changing any "tested with" claim or `versionMin=`.
