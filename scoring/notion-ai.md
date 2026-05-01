# Notion AI

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Freshness | 3 | Real-time ingestion across the Notion workspace; connector-based ingestion for external sources (Slack, Drive, GitHub, Linear, Jira) updates within minutes. No skill artifact concept means no skill-regeneration story. |
| Audience-safety | 2 | Page-level + workspace permissions, mature ACL inheritance for connected apps. Custom Agents respect permissions but have no first-class audience model — internal-only context can leak via paraphrase. |
| Portability | 0 | Output is Notion pages, Notion AI answers, or Custom Agent runs — all locked to the Notion workspace UI. No portable artifact format. Custom Agents are workspace-bound. |
| Operational provenance | 3 | Citations are preserved when the assistant cites Notion pages or connected app sources. Provenance UX is solid for content; weaker for derived knowledge (e.g., "what we decided in this thread"). |
| **Total** | **8 / 20** | |

## Architecture summary

Notion AI = AI features layered on top of the Notion workspace. The workspace itself acts as the "knowledge graph" via pages, databases, and explicit relations. Notion 3.0 added Custom Agents — natural-language workflow automations bound to a workspace, with credits-based pricing for advanced features.

Connectors (Slack, GitHub, Drive, Linear, Jira, Teams/SharePoint) bring external data into the search/Q&A surface, with citations preserved.

## What it does best

- Ubiquity. 100M+ users.
- Flexible knowledge structure where the customer already lives in Notion
- Strong creation surface — easy to write, edit, link
- Custom Agents for workspace-internal automation

## What it doesn't do

- Emit anything an external agent runtime (Claude Code, Cursor, Codex) can load
- Operate as a brain over a customer's *entire* operational signal — it operates over the Notion subset of that signal plus connected apps
- Multi-tenant brain-per-managed-client (one workspace = one customer)
- First-class audience scoping for operator-vs-customer separation

## Sources

- [Notion 3.3 release notes](https://www.notion.com/releases/2026-02-24)
- [Notion AI connectors guide (eesel)](https://www.eesel.ai/blog/notion-ai-connectors)
- [Notion pricing](https://www.notion.com/pricing)

## What would move their score

- **Portability:** allow Custom Agent definitions or workspace-derived skills to export as `SKILL.md`. Notion's database + relation structure is well-suited to skill emission; the architectural lift would be moderate.
- **Audience-safety:** add an explicit operator-only flag on databases/pages with runtime enforcement at the agent layer.
- **Freshness:** the underlying ingestion is already real-time; the score is bounded by lack of a skill-regeneration concept.

[UNCERTAIN] Custom Agents are still relatively new. Architectural details on agent context isolation across workspaces are not fully public; the audience-safety score may move up if more is published.
