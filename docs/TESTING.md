# Testing

Status: **Not yet defined**

This document owns repeatable validation procedures, not historical results.

## Test environment

- Game build: `TBD`
- Mod build/package identity: `TBD`
- Server/client topology: `TBD`
- Relevant log locations: `TBD`

## Engine logging note

Project Zomboid's client debug log is capped in place with no rotation (observed around 4.3MB on one machine): once a session's log volume crosses that line, the engine silently drops its own oldest lines rather than archiving them. A long or verbose diagnostic session can lose its early evidence this way. Keep per-event diagnostics off by default, and if a session needs verbose logging over a long run, snapshot the client log between test phases rather than relying on its final state — see [`../scripts/README.md`](../scripts/README.md) if test-cycle automation scripts exist in this repository.

## Validation matrix

Define scenario, setup, steps, expected result, authority/topology, and pass/fail criteria for each claimed feature. Include dedicated-server and save/load coverage when relevant.

Record real outcomes in [`VALIDATION_HISTORY.md`](VALIDATION_HISTORY.md).
