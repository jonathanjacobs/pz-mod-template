# Release checklist

Status: **Not relevant until preparing a release.**

Use this checklist before a public GitHub release or Steam Workshop update. Tick an item only where recorded evidence supports it; the evidence lives in [`VALIDATION_HISTORY.md`](VALIDATION_HISTORY.md). Keep the gates proportionate: require what protects players' saves and the mod's core behavior, and watch the rest during normal play.

Current release: `TBD`

## General gate

- [ ] `VERSION`, `CHANGELOG.md`, both `mod.info` files, and runtime build stamps agree, and `bash tools/validate-package.sh` passes.
- [ ] Public status, compatibility, configuration, and behavior claims match recorded evidence and state the remaining validation boundaries.
- [ ] The smoke test and core behavior test in [`TESTING.md`](TESTING.md) were run (normal-session logs count) and recorded in [`VALIDATION_HISTORY.md`](VALIDATION_HISTORY.md).
- [ ] No known high-severity save, world, player, client, or server defect is being silently shipped.
- [ ] Dedicated-server, multiplayer-authority, and save/load behavior were tested where claimed.
- [ ] The package has one runtime tree and contains no logs, saves, credentials, private configuration, source-control metadata, backups, decompiled source, or extracted game assets.
- [ ] Provenance, licensing, attribution, and the [Project Zomboid Modding Policy](PZ_MODDING_POLICY.md) review are current, and public material presents the mod as unofficial and independent.
- [ ] Installation, update, monitoring, and rollback instructions in [`DEPLOYMENT.md`](DEPLOYMENT.md) are current.
- [ ] Workshop identifiers, package layout, artwork, and metadata follow [`STEAM_WORKSHOP.md`](STEAM_WORKSHOP.md).

## Stable release gate

Only for a release labeled stable (for example `1.0.0` or later).

- [ ] Server and at least one client log from normal play show the core behavior working without a recurring error from this mod. `TBD` — name the specific transitions or outcomes that must appear.
- [ ] Known interactions and compatibility limits are documented and accepted for the release.
- [ ] Each optional feature enabled by default has passed its own check.

Watch during normal play rather than staging dedicated tests; record anything notable in [`VALIDATION_HISTORY.md`](VALIDATION_HISTORY.md), and treat a real problem here as a blocker for the next release:

- `TBD` — joins, disconnects, deaths, and respawns leaving stale state;
- `TBD` — optional presentation (notifications, UI) missing, repeated, or noisy;
- CPU cost or normal log volume becoming a problem for the server.

Rollback steps are documented in [`DEPLOYMENT.md`](DEPLOYMENT.md); they are not rehearsed as a release gate.

## Deployment gate

- [ ] Stop the server cleanly and back up world, save, and configuration before updating.
- [ ] Upload the release to the existing Workshop item, then paste [`../workshop-description.bbcode`](../workshop-description.bbcode) into the item description again (each upload replaces it with the one-line `workshop.txt` summary).
- [ ] Confirm the server and every participating client report the new build stamp after deployment.
- [ ] Preserve early release logs and use the documented rollback if a problem appears.

Release decision: **`TBD`** (`GO`, `CONDITIONAL GO` with the conditions listed, or `NO-GO`)

Review date: **`TBD`**

History: `TBD` — one line per release decision, noting what evidence satisfied the gates.
