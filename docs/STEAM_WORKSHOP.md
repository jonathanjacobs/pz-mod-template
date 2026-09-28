# Steam Workshop publication

Status: **Not yet configured**

Use this file only when the project is published through Steam Workshop; otherwise leave it as a stub or remove it together with `workshop.txt` and `workshop-description.bbcode`. This document owns Workshop packaging and update mechanics. Runtime configuration belongs in [`DEPLOYMENT.md`](DEPLOYMENT.md); release gates belong in [`RELEASE_CHECKLIST.md`](RELEASE_CHECKLIST.md); public description text is canonical in [`../workshop-description.bbcode`](../workshop-description.bbcode).

Project Zomboid Mod ID: `TBD`  
Permanent Steam Workshop ID: `TBD` (assigned on first upload)

## Package layout

A clean repository root is intentionally usable as the Project Zomboid Workshop item directory:

```text
<workshop-item>/
├── workshop.txt
├── workshop-description.bbcode
├── preview.png
├── Contents/
│   └── mods/
│       └── <mod-id>/
│           ├── mod.info
│           ├── common/
│           └── 42/
│               ├── mod.info
│               ├── poster.png
│               ├── icon.png
│               └── media/
├── README.md, CHANGELOG.md, docs/
└── public licensing and provenance files
```

There is one authoritative deployable runtime tree, `Contents/mods/<mod-id>/`. Do not create a second root-level `42/`, `common/`, or runtime `mod.info` copy.

Public documentation may be included intentionally. `.git/`, logs, saves, credentials, private configuration, local test artifacts, backups, decompiled source, and scratch material must never be copied into the authoring directory. `git archive HEAD | tar -x -C <authoring-dir>` exports only tracked files, which keeps all of those out; tracked docs and development tooling come along with it, which is harmless.

## `workshop.txt`

The root [`../workshop.txt`](../workshop.txt) holds the uploader metadata:

- `id=` — absent until the first upload creates the item; the uploader then writes it. Commit it and never change it afterward.
- `title=` — the public item title.
- `description=` — a one-line summary. The in-game uploader writes this line over the Steam description on **every** upload (see below).
- `tags=` — Workshop tags such as `Build 42` and `Multiplayer`.
- `visibility=` — `private` until the first public release, then `public`.

[`../tools/validate-package.sh`](../tools/validate-package.sh) treats a numeric `id=` as the signal that the project is publishing, and from then on requires the artwork below and a placeholder-free Workshop description.

## Artwork

| File | Purpose | Checked by the validator |
| --- | --- | --- |
| `preview.png` (item root) | Workshop uploader preview | PNG, 256×256, at most 1000 KB |
| `Contents/mods/<mod-id>/42/poster.png` | In-game mod-manager poster, referenced by `poster=` | PNG identity |
| `Contents/mods/<mod-id>/42/icon.png` | In-game mod-list icon, referenced by `icon=` | PNG identity |

Record the provenance of every image in [`../ASSET_LICENSE.md`](../ASSET_LICENSE.md). Do not silently resize publication artwork as part of an unrelated code release.

## Stable identities

Routine updates must reuse the same Workshop item. Never create a new Workshop item merely to publish a version update.

A Steam-backed dedicated server uses both identifiers:

```text
WorkshopItems=<workshop-id>
Mods=<mod-id>
```

The Workshop ID selects the Steam package; the Mod ID is what Project Zomboid loads.

## Canonical Workshop description

Maintain the paste-ready Steam BBCode in [`../workshop-description.bbcode`](../workshop-description.bbcode). When public behavior or status changes materially, update that file in Git and then paste it into the existing Steam item. Do not maintain a separate prose description in this guide.

- **Every upload replaces the Steam description** with the one-line `description=` summary from `workshop.txt`. Paste the full BBCode again after each upload.
- Steam does not render `[center]` or `[br]`; they appear as literal text. Use blank lines for spacing. The validator rejects both tags.
- Replace every bracketed `[PLACEHOLDER]` before the first publication; the validator rejects leftovers once an `id=` exists.
- An optional support/donation section is allowed, provided donations unlock nothing — see rule 6 in [`PZ_MODDING_POLICY.md`](PZ_MODDING_POLICY.md). Host any button image on an external image host and link it with `[url=...][img]...[/img][/url]`.

Required public disclosures and provenance checks are governed by [`PZ_MODDING_POLICY.md`](PZ_MODDING_POLICY.md) and [`RELEASE_CHECKLIST.md`](RELEASE_CHECKLIST.md).

## Update workflow

1. Complete source and runtime changes; update `VERSION`, both `mod.info` files, `CHANGELOG.md`, and the Workshop description as appropriate. Run `bash tools/validate-package.sh`.
2. Complete [`RELEASE_CHECKLIST.md`](RELEASE_CHECKLIST.md).
3. Prepare a clean authoring directory under `Zomboid/Workshop/` from the repository (see [Package layout](#package-layout)).
4. Preserve the Workshop ID in `workshop.txt`.
5. Use Project Zomboid **Workshop → Create and Update Items** to update the existing item.
6. Write an accurate Steam change note (BBCode is supported). If the uploader does not carry it over, add or edit it on the item's Steam **Change Notes** tab.
7. Paste [`../workshop-description.bbcode`](../workshop-description.bbcode) into the item description again.
8. Verify the distributed package rather than the authoring copy: the dedicated server's Workshop download should log the new build stamp, and a player client should report the matching server build (see the build-stamp convention in [`ARCHITECTURE.md`](ARCHITECTURE.md)).
9. Run the smoke test in [`TESTING.md`](TESTING.md).

**Do not subscribe to the Workshop item on the machine that holds the `Zomboid/Workshop` authoring copy.** The subscribed copy and the authoring copy share the Mod ID, and the game can mix files from both, so older Lua or sandbox options may load alongside the new version. Verify the published package from the dedicated server or from a client without the authoring copy.

## Post-publication verification

Confirm:

- the expected `Contents/mods/<mod-id>/` runtime tree is present;
- `mod.info` metadata and version are correct;
- preview, poster, and icon load as intended;
- the dedicated server acquires the updated item and clients receive the same package version;
- the smoke test in [`TESTING.md`](TESTING.md) passes;
- rollback instructions in [`DEPLOYMENT.md`](DEPLOYMENT.md) remain accurate.
