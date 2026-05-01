# BizBrain OS

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Freshness | 4 | Continuous ingestion across Gmail, Slack, WhatsApp, Drive, meeting transcripts, and manual files. Skill artifacts auto-regenerate when source provenance changes. We have not yet shipped full bitemporal queries (`what did we believe on March 1?` is not yet a one-call API), so this is a 4 not a 5. We expect to close this gap in v0.5 of the brain runtime. |
| Audience-safety | 5 | First-class audience primitive (`internal` / `client_safe` / `public`) on every fact, entity, and emitted skill. Hook-gated at write time (the comms gate refuses to publish operator-only data into client-facing channels), runtime-gated at load time (the parser refuses to load `internal`-audience skills into `client_safe` sessions), audit logged. We have not shipped cryptographic signing of audience scope (a 5 in the strict-regulatory sense), but the operational enforcement is complete and we have not had a leakage incident in production. |
| Portability | 4 | Emit Anthropic-compatible `SKILL.md` files via the open `brain-skill-bundle` spec ([github.com/.../brain-skill-bundle](#)). Strict superset of agentskills.io — runtimes that don't speak the extension load the file as a normal Anthropic skill. AGENTS.md export coming. Not a 5 because cross-vendor adoption of the extension blocks (tenancy/audience/provenance) is still nascent — we're the only implementation. |
| Operational provenance | 4 | Every emitted skill tracks `provenance.sources` pointing to the originating Gmail thread, Slack channel, Drive file, or meeting transcript. Survives skill regeneration. We have not shipped cryptographic source proofs (a 5), so a determined adversary could in principle forge a provenance pointer; this is on the v0.6 roadmap. |
| **Total** | **17 / 20** | |

## Architecture summary

BizBrain OS is a multi-tenant company-brain platform running across paying clients. Each tenant gets a structurally isolated brain with:

- **Per-tenant ingestion** — Gmail, Slack, WhatsApp, Drive, meeting transcripts, manual files
- **Entity store** — Clients, Partners, Vendors, People, Projects, Decisions, plus auto-evolved types per tenant (the dental tenant got `Patients` from observed patterns; the construction tenant got `Jobs`)
- **Schema evolution agent** — detects misfit patterns, accumulates confidence, proposes new record types at threshold with a 24-hour undo window
- **Internal/external separation** — `_internal/` for operator-only data, hook-gated at write, runtime-gated at load
- **Knowledge graph (Graphify)** — temporal, queryable, with Obsidian vault interop
- **Skill emission** — `SKILL.md` files via the `brain-skill-bundle` spec; auto-regenerate on source-provenance changes

The platform sits inside C² Advisory's managed-services delivery — the consulting firm is the operator, paying business clients are the tenants. C² is both the wedge and the proof — the brain is the substrate every C² engagement runs on, and every engagement is a paying integration test for the platform.

## What it does best

- Multi-tenant brain-per-managed-client at the architecture level (not as a sales motion)
- First-class audience scoping with runtime enforcement
- Auto-evolving schema with confidence thresholds
- Live-comms ingestion as primary signal (not document-uploads as primary signal)
- Portable skill-file emission via an open spec

## What it doesn't do well yet

- **Bitemporal queries.** We track `valid_from` / `valid_to` on facts but the query API is not yet first-class. v0.5.
- **Cryptographic audience signing + provenance proofs.** The operational enforcement is complete; the cryptographic layer is on the v0.6 roadmap.
- **Distribution.** We have a managed-services book of business, not 200 enterprise customers. Glean wins on distribution by an order of magnitude.
- **F500 customer logos.** We don't have them. Mid-market is our band.

## Sources

- [`brain-skill-bundle` spec + reference parser]
- [BizBrain OS demo URL]
- [Technical writeup: "What we learned shipping multi-tenant company brains"]

## What would move our score to 20

- **Freshness 5:** ship the first-class bitemporal query API
- **Audience-safety 5:** add cryptographic signing of audience scope on emitted skills, with a verifier in the reference parser
- **Portability 5:** get at least 3 independent runtimes (Cursor, Codex, Lindy, Devin, OpenAI Agents SDK) to support the `brain-skill-bundle` extension blocks natively
- **Provenance 5:** add cryptographic source proofs that survive ingestion and skill regeneration

We expect to ship freshness 5 by Q3 2026, audience-safety 5 by Q4, portability 5 dependent on partnerships, provenance 5 by 2027.

## Honesty note

We score ourselves first because we wrote the rubric. The rubric reflects what we built BizBrain OS against — the requirements list of running multi-tenant brains in production. **If a future product beats us on these dimensions, this benchmark says so honestly.** Open an issue.
