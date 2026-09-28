# Design

Status: **Not yet defined**

This document has two parts with different authority. **Requirements** state what the mod must do, as players and server operators see it. **Architecture** describes how the current implementation does it. Keep them separate: an implementation detail is not a requirement until it is written into the requirements section, and a requirement does not change because the code happens to behave differently.

## Requirements

### Project identity

- Mod name: `TBD`
- Mod ID: `TBD`
- Target Build: `TBD`
- Primary supported mode: `TBD` (single-player, dedicated multiplayer, or both)

### Scope

- In scope: `TBD`
- Explicitly out of scope: `TBD`

### Behavior

Add numbered, testable requirements (`R1`, `R2`, …) so tests, commits, and issues can cite them. State authority, save/load expectations, compatibility assumptions, configuration defaults, and failure behavior where relevant.

- `R1` — `TBD`

## Architecture

Cover module responsibilities, Lua client/server/shared boundaries, persistence, networking, configuration, and diagnostics once a design exists. Record a decision with realistic alternatives as an ADR under [`adr/`](adr/).

### Runtime layout

```text
Contents/mods/<mod-id>/
  mod.info
  common/
    media/
  42/
    mod.info
    poster.png
    icon.png
    media/
      lua/
        client/
        server/
        shared/
          Translate/EN/
      sandbox-options.txt
```

Build 42 expects both a `common/` folder and a build-specific `42/` folder beside the root `mod.info`. Git does not track empty directories, so the template keeps them with `.gitkeep` placeholders under `media/AnimSets/` and `media/actiongroups/`; leave those in place until real content occupies the folders.

Both `mod.info` files carry the same `id=`, `name=`, `description=`, `author=`, `category=`, `modversion=`, and `versionMin=` values. The build-specific `42/mod.info` also references `poster=` and `icon=` artwork. Use `modversion=` for the mod's release version (not `version=`), and set `versionMin=` to the oldest Project Zomboid build the mod has actually been tested on. Keep `modversion=` equal to [`../VERSION`](../VERSION); the package validator checks this.

There is one authoritative runtime tree. Do not create a second root-level `42/`, `common/`, `media/`, or `mod.info` copy.

### Build stamp and version handshake

Recommended from the first multiplayer build. Mixed-version installs — a stale local copy beside the Workshop copy, a client that has not downloaded the update, or a server that has not restarted — are a common cause of confusing test results, and they are invisible unless the mod reports which build is running.

- Define the build version once, in a shared module (for example `42/media/lua/shared/<ModName>/Version.lua` returning `{ BUILD_VERSION = "x.y.z" }`), and `require` it wherever the version is needed. Keep it equal to [`../VERSION`](../VERSION); [`../tools/validate-package.sh`](../tools/validate-package.sh) rejects any `BUILD_VERSION = "..."`, `buildVersion = "..."`, or `Loaded vX.Y.Z` literal in runtime Lua that disagrees.
- **Server:** log the build and the effective configuration once at startup, for example `[<ModName>] CONFIG | build=x.y.z | <key settings>`.
- **Server to client:** include `buildVersion` in the first state message each client receives.
- **Client:** log `[<ModName>] SERVER_BUILD | x.y.z` once on receipt, and log `BUILD_MISMATCH | client=… | server=…` once if it differs from the client's own build.

With this in place, confirming that everyone runs the same package is a log search rather than a guess, and it is the first step in [`TESTING.md`](TESTING.md#before-testing) and in post-release verification.

### Components

`TBD`
