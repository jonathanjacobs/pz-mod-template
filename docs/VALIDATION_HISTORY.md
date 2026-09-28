# Validation history

Status: **No validation has been recorded.**

Record only tests that actually occurred. Each entry should identify the date, package/version, game build, topology, procedure or scenario, observed outcome, logs/evidence location, and follow-up decision.

This is an append-only ledger. If a later run overturns an earlier entry, add a new dated entry that says so — correcting or withdrawing the earlier finding — rather than editing history.

Do not place planned tests here; use [`TESTING.md`](TESTING.md) or [`ROADMAP.md`](ROADMAP.md).

| Date | Version | Scope | Outcome | Evidence |
| --- | --- | --- | --- | --- |
| `TBD` | `TBD` | `TBD` | `TBD` | `TBD` |

The table is an index; put anything longer than a line in a dated section below it.

## Compatibility checkpoint template

Add one of these whenever a Project Zomboid update is tested, before updating any "tested with" claim or `versionMin=`.

```markdown
## Project Zomboid <version> compatibility checkpoint — <YYYY-MM-DD>

Server updated to Project Zomboid `<version>` revision `<revision>` with mod build `<x.y.z>`. Reviewed: <which server and client logs, from what window>.

Observed evidence:

- server and client both reported `<version> <revision>`, and the client received `SERVER_BUILD | <x.y.z>`;
- every module of this mod loaded without a Lua exception;
- <core behavior observed, with the relevant log values>;
- no anti-cheat warning, kick, or rejected packet appeared around the mod's activity.

Decision: <PASS / FAIL / PASS with conditions> for <which tests in TESTING.md>.

**Evidence boundary:**
- <what did not occur during the window and is accepted on other grounds, or remains unverified>;
- <which players' logs were not reviewed>.
```
