# Project Zomboid Modding Policy compliance

Do not update for: an individual asset or piece of third-party material (record it in [`../CREDITS.md`](../CREDITS.md)).

This project is intended for work under The Indie Stone's current Project Zomboid Modding Policy and applicable distribution-platform rules. This document is the project's engineering and release-control policy; it does not replace the authoritative policy:

- <https://projectzomboid.com/blog/modding-policy/>

A project created from this template is an unofficial independent community mod; nothing in it implies affiliation with or endorsement by The Indie Stone.

Last reviewed: **Not yet reviewed for a release**

## Mandatory rules

These apply from the first commit, not just at release.

1. Added code, art, audio, models, text, data, and tools must be original or have documented redistribution rights.
2. Public availability of another mod does not permit copying or redistribution.
3. Record every distributed asset and every piece of third-party material in [`../CREDITS.md`](../CREDITS.md) when it is added.
4. Prefer runtime references to vanilla APIs and identifiers over extracting or copying Project Zomboid assets.
5. Do not imply official status or endorsement by The Indie Stone.
6. Do not add paid/donor-exclusive functionality, malicious behavior, licensing circumvention, piracy support, or unauthorized modpack redistribution.
7. Describe material behavior changes accurately in release notes and Workshop material.

## License boundary

The repository license applies only to material the project has the right to license. It does not relicense Project Zomboid or third-party material.

## Release checks

Part of the [release checklist](RELEASING.md#release-checklist):

- Before the first public release, recheck the live policy and update the review date above.
- [`../CREDITS.md`](../CREDITS.md) covers every distributed file that is not original code.
- Public material (README, Workshop description, `mod.info`) presents the mod as unofficial and independent.
