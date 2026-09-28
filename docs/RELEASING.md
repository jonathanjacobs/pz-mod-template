# Releasing

Status: **Not relevant until preparing a release.**

This document owns how a version gets from the repository to players: the release checklist, Steam Workshop publication, post-release checks, and rollback. Player-facing installation and configuration live in [`../README.md`](../README.md); public Workshop text is canonical in [`../workshop-description.bbcode`](../workshop-description.bbcode). If the mod is not published on the Workshop, delete the Workshop sections along with `workshop.txt` and `workshop-description.bbcode`.

Project Zomboid Mod ID: `TBD`  
Permanent Steam Workshop ID: `TBD` (assigned on first upload)

## Release checklist

Tick an item only where recorded evidence supports it; evidence lives in [`VALIDATION_HISTORY.md`](VALIDATION_HISTORY.md). Require what protects players' saves and the mod's core behavior, and watch the rest during normal play.

- [ ] `VERSION`, `CHANGELOG.md`, both `mod.info` files, the README, the Workshop text, and runtime build stamps agree — `bash tools/validate-package.sh` passes.
- [ ] The smoke test and core behavior test in [`TESTING.md`](TESTING.md) passed on this build (normal-session logs count) and are recorded in [`VALIDATION_HISTORY.md`](VALIDATION_HISTORY.md).
- [ ] Multiplayer authority and save/load behavior were tested wherever the public text claims them.
- [ ] No known high-severity save, world, player, client, or server defect is being shipped silently.
- [ ] Public claims (status, compatibility, "tested with", configuration) match the recorded evidence.
- [ ] Every distributed asset and any third-party material is recorded in [`../CREDITS.md`](../CREDITS.md), and the [modding-policy checks](PZ_MODDING_POLICY.md#release-checks) are done.
- [ ] Rollback below is still accurate for this release.

A **stable** release (`1.0.0` or later) additionally needs server and client logs from normal play showing the core behavior with no recurring error from this mod.

Watch these during normal play rather than staging tests for them, record anything notable in [`VALIDATION_HISTORY.md`](VALIDATION_HISTORY.md), and treat a real problem as a blocker for the next release: joins, disconnects, deaths, and respawns leaving stale state; optional presentation (notifications, UI) missing or noisy; CPU cost or log volume becoming a problem for the server.

## Publishing to Steam Workshop

1. Stop the test server cleanly, and back up the world, save, and configuration of any server you will update.
2. Prepare a clean authoring directory under `Zomboid/Workshop/<item-name>/` from the repository, for example `git archive HEAD | tar -x -C <authoring-dir>`. That exports only tracked files, which keeps `.git/`, logs, saves, credentials, and decompiled source out; tracked docs and tooling come along, which is harmless.
3. In Project Zomboid, use **Workshop → Create and Update Items** to update the existing item. Never create a new item for a routine update.
4. Write an accurate change note (BBCode works). If the uploader does not carry it over, add or edit it on the item's Steam **Change Notes** tab.
5. **Paste [`../workshop-description.bbcode`](../workshop-description.bbcode) into the item description again.** Every upload replaces the Steam description with the one-line `description=` summary from `workshop.txt`.
6. After the first upload only: commit the `id=` line the uploader wrote into `workshop.txt`, and record the Workshop ID above and in [`../AGENTS.md`](../AGENTS.md).

**Do not subscribe to the item on the machine that holds the authoring copy.** The subscribed and authoring copies share the Mod ID, and the game can load files from both, so older Lua or sandbox options may run alongside the new version. Verify from the dedicated server or from a client without the authoring copy.

## After publishing

1. The dedicated server downloads the update and logs the new `CONFIG | build=` line; a client reports the matching `SERVER_BUILD` with no `BUILD_MISMATCH` (see the build-stamp convention in [`DESIGN.md`](DESIGN.md#build-stamp-and-version-handshake)).
2. Poster, icon, and preview show as intended.
3. The smoke test in [`TESTING.md`](TESTING.md) passes on the live server.
4. Keep the early server and client logs from the release in case a problem appears.

## Rollback

`TBD` — fill in once there is something to roll back:

- **Per feature:** which sandbox option turns off each optional feature while leaving the core behavior running. Prefer this before removing the mod.
- **Whole mod:** how to remove the mod or return to a previous version, what happens to saved state the mod created, and whether existing worlds load cleanly without it.

## Workshop reference

### Package layout

A clean repository root doubles as the Workshop item directory:

```text
<workshop-item>/
├── workshop.txt
├── workshop-description.bbcode
├── preview.png
├── Contents/mods/<mod-id>/      (the only runtime tree; see DESIGN.md)
└── README.md, CHANGELOG.md, docs/, licensing files
```

### `workshop.txt`

- `id=` — absent until the first upload writes it; never change it afterward. [`../tools/validate-package.sh`](../tools/validate-package.sh) treats a numeric `id=` as the signal that the project is publishing, and from then on requires the artwork below and a placeholder-free Workshop description.
- `title=` — the public item title.
- `description=` — the one-line summary that overwrites the Steam description on every upload.
- `tags=` — Workshop tags such as `Build 42` and `Multiplayer`.
- `visibility=` — `private` until the first public release, then `public`.

### Artwork

| File | Purpose | Checked by the validator |
| --- | --- | --- |
| `preview.png` (item root) | Workshop uploader preview | PNG, 256×256, at most 1000 KB |
| `Contents/mods/<mod-id>/42/poster.png` | In-game mod-manager poster (`poster=`) | PNG identity |
| `Contents/mods/<mod-id>/42/icon.png` | In-game mod-list icon (`icon=`) | PNG identity |

Record the provenance of every image in [`../CREDITS.md`](../CREDITS.md). Do not silently resize publication artwork as part of an unrelated code release.

### Workshop description

- Update [`../workshop-description.bbcode`](../workshop-description.bbcode) in Git when public behavior or status changes, then paste it into the item. Do not keep a second copy of the description anywhere else.
- Steam does not render `[center]` or `[br]`; they show as literal text. Use blank lines for spacing. The validator rejects both.
- Replace every bracketed `[PLACEHOLDER]` before the first publication.
- An optional support or donation section is allowed as long as donations unlock nothing (rule 6 in [`PZ_MODDING_POLICY.md`](PZ_MODDING_POLICY.md)). Host any button image externally and link it with `[url=...][img]...[/img][/url]`.
