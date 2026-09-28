# Testing

Status: **Not yet defined**

This document owns repeatable test procedures, not historical results. Record real outcomes in [`VALIDATION_HISTORY.md`](VALIDATION_HISTORY.md); expected behavior lives in the requirements in [`DESIGN.md`](DESIGN.md#requirements); long experimental procedures belong in [`spikes/`](spikes/).

Keep this guide short and proportionate to a hobby mod. Logs from normal play count as evidence; stage a dedicated test only when normal play does not cover a change. Replace each `TBD` below with the project's own checks, and delete sections that do not apply.

## Contents

- [Before testing](#before-testing)
- [Smoke test](#smoke-test)
- [Core behavior test](#core-behavior-test)
- [Feature checks](#feature-checks)
- [After a Project Zomboid update](#after-a-project-zomboid-update)
- [Chasing a problem](#chasing-a-problem)
- [Engine logging note](#engine-logging-note)

## Before testing

- `bash tools/validate-package.sh` passes for the build under test.
- Server and clients show the same Project Zomboid `version=` / `revision=` line and the same mod build (server `CONFIG | build=`, client `SERVER_BUILD`, and no `BUILD_MISMATCH`; see the build-stamp convention in [`DESIGN.md`](DESIGN.md#build-stamp-and-version-handshake)).
- Only one copy of the mod is installed on each machine. A local copy and a Workshop copy with the same Mod ID can load mixed Lua and sandbox-option versions, which makes every result untrustworthy.
- Note the active sandbox settings; expected results use the active settings, not the shipped defaults.

## Smoke test

Run after any change, new release, or Project Zomboid update.

1. The server starts and a client joins with no Lua errors from this mod on either side.
2. `TBD` — the mod's core behavior is present in its simplest form.
3. Disabled optional features stay quiet, and diagnostics produce no output while off.

## Core behavior test

Run when the core behavior may have changed. A normal session that exercises the behavior counts.

1. `TBD`

## Feature checks

Run a check only when that feature changes.

- **`TBD` feature:** `TBD` expected observation.

## After a Project Zomboid update

1. Skim the patch notes and modding news for changes to the systems this mod touches.
2. Run the smoke test, and the core behavior test if a touched system changed.
3. Check the server log for anti-cheat warnings, kicks, or rejected packets around the mod's activity.
4. Record a compatibility checkpoint in [`VALIDATION_HISTORY.md`](VALIDATION_HISTORY.md). Update "tested with" claims in `README.md`, the Workshop description, and `versionMin=` only after it is recorded.

## Chasing a problem

1. Save the normal server and client logs around the event.
2. Turn on the mod's diagnostics, reproduce once, then turn them off again.
3. Collect the server console/DebugLog and the affected client's DebugLog. `TBD` — name the log prefix this mod uses.

If an optional layer is the suspect, turn it off first using the rollback steps in [`RELEASING.md`](RELEASING.md#rollback).

## Engine logging note

Project Zomboid's client debug log is capped in place with no rotation (observed around 4.3MB on one machine): once a session's log volume crosses that line, the engine silently drops its own oldest lines rather than archiving them. A long or verbose diagnostic session can lose its early evidence this way. Keep per-event diagnostics off by default, and if a session needs verbose logging over a long run, snapshot the client log between test phases rather than relying on its final state — see [`../scripts/README.md`](../scripts/README.md) if test-cycle automation scripts exist in this repository.
