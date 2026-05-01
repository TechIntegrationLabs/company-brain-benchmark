# Glean

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Freshness | 3 | Continuous ingestion via 100+ connectors; updates propagate within minutes-to-hours. No automatic skill regeneration because the output is search/answers, not skill artifacts. |
| Audience-safety | 3 | Inherits permissions from source systems (Drive, Slack, Confluence). Strong at document-level ACLs. No first-class audience primitive at the artifact layer; vulnerable to paraphrase leakage when the assistant summarizes internal-only content. |
| Portability | 1 | Output is search results + assistant answers inside Glean's UI. No portable skill-file emission. Some API access for data export but no cross-runtime artifact format. |
| Operational provenance | 4 | Strong citation surface — every answer links to source document. Mature provenance UX for docs and chat. Slightly weaker on meeting-transcript provenance (depends on customer's transcription source). |
| **Total** | **11 / 20** | |

## Architecture summary

Glean ingests via 100+ connectors (Slack, GitHub, Confluence, Notion, Drive, Salesforce, Jira, Zendesk, etc.). Builds three layered graphs: knowledge graph (content), people graph (org), activity graph (usage signals). Permissions inherited from source systems with optional customer-hosted single-tenant deployment for regulated buyers.

Recent additions (2025): Agentic Engine 2 (multi-step reasoning over the graph), Canvas (collaborative AI workspace), Enterprise Flex pricing (per-user/month + pooled credits for advanced AI usage).

## What it does best

- Permissioned enterprise search at scale (200+ enterprise customers)
- Cross-system retrieval where the answer requires synthesizing across SaaS apps
- Citation provenance for documents

## What it doesn't do

- Emit portable skill files an external agent runtime can load
- First-class audience scoping beyond source-system ACLs
- Auto-evolving schema (the knowledge graph is essentially fixed entity types)
- Multi-tenant brain-per-managed-client (each Glean deployment is single-tenant per customer)

## Sources

- [Glean Series F announcement](https://www.glean.com/blog/glean-series-f-announcement)
- [Glean ARR doubled to $200M (Futurum)](https://futurumgroup.com/insights/glean-doubles-arr-to-200m-can-its-knowledge-graph-beat-copilot/)
- [Glean Enterprise Search 2025 Guide](https://www.glean.com/blog/the-definitive-guide-to-ai-based-enterprise-search-for-2025)
- [Glean Press: 3rd-gen AI Assistant](https://www.glean.com/press/glean-introduces-third-generation-ai-assistant-new-enterprise-graph-to-enable-the-superintelligent-enterprise)

## What would move their score

- **Portability:** ship a documented `SKILL.md` (or equivalent) export. Today there's no path to a portable artifact.
- **Audience-safety:** add a first-class operator-vs-customer-safe metadata layer above source-system ACLs. Glean has the infrastructure; they just don't expose it as a primitive.
- **Freshness:** add skill-regeneration triggers on source changes (most of the data plumbing is already there).
