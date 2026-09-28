# Architecture

Status: **Not yet defined**

Document the implementation once a design exists. Cover module responsibilities, Lua client/server/shared boundaries, persistence, networking, configuration, and diagnostics. Link to an ADR for durable decisions with meaningful alternatives.

## Runtime layout

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

## Design

`TBD`
