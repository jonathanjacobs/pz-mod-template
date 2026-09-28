# Documentation ownership

This file defines where mutable project information belongs so the repository does not maintain competing copies of the same facts.

| Information | Canonical source |
| --- | --- |
| Public overview, installation, configuration reference, and release identity | [`../README.md`](../README.md), [`../VERSION`](../VERSION), and [`../CHANGELOG.md`](../CHANGELOG.md) |
| Normative behavior (requirements) and implementation design (architecture) | [`DESIGN.md`](DESIGN.md), with durable decisions in [`adr/`](adr/) |
| Milestones, sequencing, and current work | [`ROADMAP.md`](ROADMAP.md) |
| Individual defects and open design questions | GitHub Issues, cited by number elsewhere |
| Repeatable test procedure | [`TESTING.md`](TESTING.md) |
| Actual test outcomes | [`VALIDATION_HISTORY.md`](VALIDATION_HISTORY.md) |
| Experimental evidence | [`spikes/`](spikes/) |
| Release checklist, Workshop publication, and rollback | [`RELEASING.md`](RELEASING.md) |
| Public Workshop text | [`../workshop-description.bbcode`](../workshop-description.bbcode) and [`../workshop.txt`](../workshop.txt) |
| Modding-policy rules | [`PZ_MODDING_POLICY.md`](PZ_MODDING_POLICY.md) |
| Asset and third-party provenance | [`../CREDITS.md`](../CREDITS.md) |
| License and attribution notices | [`../LICENSE`](../LICENSE) and [`../NOTICE`](../NOTICE) |
| External reference links and mods studied for ideas | [`RESEARCH_LINKS.md`](RESEARCH_LINKS.md) |
| Agent working rules and current development context | [`../AGENTS.md`](../AGENTS.md) (imported by [`../CLAUDE.md`](../CLAUDE.md), which holds no rules of its own) |
| Package validation | [`../tools/validate-package.sh`](../tools/validate-package.sh), documented in [`../tools/README.md`](../tools/README.md) |
| Test-cycle automation | [`../scripts/README.md`](../scripts/README.md) |

## Where to start by reader

- Server operators and players: [`../README.md`](../README.md)
- Contributors: [`DESIGN.md`](DESIGN.md) and [`ROADMAP.md`](ROADMAP.md)
- Testers: [`TESTING.md`](TESTING.md) and [`VALIDATION_HISTORY.md`](VALIDATION_HISTORY.md)
- Release maintainers: [`RELEASING.md`](RELEASING.md)

## Duplication rule

Repeat a small fact only when necessary for immediate usability or safety. Do not duplicate complete specifications, validation tables, experimental narratives, roadmaps, or configuration explanations that already have a canonical home.

Update the canonical source first when behavior changes; replace secondary detail with a link where practical.

Known overlaps and how they are resolved:

- **README and Workshop description.** The README owns the full configuration reference. The Workshop description is read on Steam without the repository, so it may carry a shorter summary of the same settings; update it whenever the README's public behavior changes.
- **ROADMAP and GitHub Issues.** Issues own individual defects and questions. The roadmap owns order and milestones and cites issue numbers rather than restating them.
- **AGENTS.md "Current development context" and ROADMAP.** AGENTS.md holds what an agent must know before touching anything (branch roles, evidence limits, environment traps). The roadmap holds the work itself.
- **CHANGELOG and VALIDATION_HISTORY.** The changelog says what changed between releases; validation history says what was observed in tests. Neither repeats the other's detail.
