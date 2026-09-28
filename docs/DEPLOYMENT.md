# Deployment

Status: **Not yet defined**

This document owns how a server operator installs, configures, updates, monitors, and rolls back this mod. Workshop packaging and upload mechanics live in [`STEAM_WORKSHOP.md`](STEAM_WORKSHOP.md); the release gate lives in [`RELEASE_CHECKLIST.md`](RELEASE_CHECKLIST.md). Delete sections that do not apply.

## Normal server configuration

`TBD` — the recommended sandbox settings for ordinary play, with safe defaults and a one-line explanation of each. Keep diagnostic options off.

```text
<ModName>.Enabled=true
<ModName>.DiagnosticsEnabled=false
```

## Steam Workshop server setup

```text
WorkshopItems=<workshop-id>
Mods=<mod-id>
```

The Workshop ID selects the Steam package; the Mod ID is what Project Zomboid loads.

## Update procedure

1. Stop the server cleanly and back up the world, save, and server configuration.
2. Remove any duplicate local copy of the mod that shares the Mod ID with the Workshop copy.
3. Update the Workshop item or install the new package.
4. Start the server and confirm every module of this mod loads without a Lua exception, and that the server logs the expected `CONFIG | build=` line.
5. Join with a client and confirm it reports the matching `SERVER_BUILD` with no `BUILD_MISMATCH`.
6. `TBD` — confirm the core behavior during the first natural occurrence in normal play.
7. Preserve early session logs after a material runtime update.

## Routine monitoring

`TBD` — the log lines an operator should expect in normal play, what healthy volume looks like, and which lines indicate a problem.

## Focused diagnostics

`TBD` — how to enable diagnostics for a short evidence window, what they log, and why they must be turned off afterward. Verbose logs can crowd out early evidence under the client log cap described in [`TESTING.md`](TESTING.md#engine-logging-note).

## Soft rollback

`TBD` — for each optional feature, which setting disables it independently while leaving the core behavior running. Prefer soft rollback before removing the mod.

## Full rollback

`TBD` — how to remove the mod or return to a previous version safely, including what happens to saved state the mod created and whether existing worlds load cleanly without it.

## Operational boundary

`TBD` — what the mod does not do or does not support (for example single-player, specific mod combinations, or other game builds).
