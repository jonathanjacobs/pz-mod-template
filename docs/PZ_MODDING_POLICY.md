# Project Zomboid Modding Policy compliance

This document is an engineering and release-control policy. It does not replace The Indie Stone's authoritative policy:

- <https://projectzomboid.com/blog/modding-policy/>

Last reviewed: **Not yet reviewed for a release**

## Mandatory rules

1. Added code, art, audio, models, text, data, and tools must be original or have documented redistribution rights.
2. Public availability of another mod does not permit copying or redistribution.
3. Record every distributed third-party component in `THIRD_PARTY_NOTICES.md` before release.
4. Prefer runtime references to vanilla APIs and identifiers over extracting or copying Project Zomboid assets.
5. Do not imply official status or endorsement by The Indie Stone.
6. Do not add paid/donor-exclusive functionality, malicious behavior, licensing circumvention, piracy support, or unauthorized modpack redistribution.
7. Describe material behavior changes accurately in release notes and Workshop material.

## License boundary

The repository license applies only to material the project has the right to license. It does not relicense Project Zomboid or third-party material.

## Release gate

Before the first public release, recheck the live policy, verify provenance for every distributed file, and complete [`RELEASE_CHECKLIST.md`](RELEASE_CHECKLIST.md).
