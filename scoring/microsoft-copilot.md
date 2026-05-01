# Microsoft 365 Copilot + Loop

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Freshness | 4 | Microsoft Graph is a real-time substrate; Copilot grounding is current within seconds for tenant content. SharePoint Embedded containers for Loop/Pages/Notebooks are tenant-scoped and current. Federated connectors extend to non-Microsoft sources. |
| Audience-safety | 4 | Mature compliance stack: Microsoft 365 permissions, sensitivity labels, DLP, audit logs. Loop respects label-based protections. Strong at "this customer cannot see content marked Confidential," weaker at the artifact layer (no first-class operator/customer skill audience model). |
| Portability | 0 | Output is locked to Microsoft 365 surfaces — Word, Outlook, Teams, Copilot Chat, Loop pages. No portable skill-file artifact for non-Microsoft agent runtimes. Copilot agents (built in Copilot Studio) run only inside the Copilot ecosystem. |
| Operational provenance | 4 | Strong citation surface across Word, Excel, PowerPoint, Teams. Cites file + line / row / slide. Microsoft Graph search results carry provenance through to Copilot responses. Some weakness on transcript-derived facts. |
| **Total** | **12 / 20** | |

## Architecture summary

Microsoft 365 Copilot grounds prompts in Microsoft Graph (the customer's M365 tenant data). External data is brought in via Graph connectors (federated retrieval) or by being indexed into Graph. Copilot Studio extends this with custom agents that can use enterprise data + Power Platform + custom plugins.

Loop / Copilot Pages / Notebooks store collaborative AI artifacts in SharePoint Embedded containers, inheriting M365 governance.

## What it does best

- Distribution. 400M+ M365 seats. Copilot is the default AI for half the planet's enterprises.
- Compliance + permissions stack is the most mature in the market
- Microsoft Graph grounding works seamlessly for tenants already in M365

## What it doesn't do

- Emit a portable skill artifact that runs outside the Microsoft stack
- Brain-per-managed-client architecture (Copilot is single-tenant per M365 customer, with strict tenant isolation as a feature)
- Auto-evolving schema (Microsoft Graph entity types are essentially fixed)
- Operate effectively where the customer's knowledge lives outside M365 (covers via federated connectors, but with weaker provenance + freshness)

## Sources

- [Microsoft Copilot architecture (MS Learn)](https://learn.microsoft.com/en-us/copilot/microsoft-365/microsoft-365-copilot-architecture)
- [Microsoft 365 Copilot permissions](https://learn.microsoft.com/en-us/copilot/microsoft-365/microsoft-365-copilot-permissions)
- [SharePoint at 25 (Microsoft Blog)](https://www.microsoft.com/en-us/microsoft-365/blog/2026/03/02/sharepoint-at-25-how-microsoft-is-putting-knowledge-to-work-in-the-ai-era/)
- [Microsoft 2026 M365 conference reveals](https://windowsnews.ai/article/microsoft-2026-m365-conference-reveals-ai-evolution-from-copilot-assistants-to-governed-autonomous-a.414501)

## What would move their score

- **Portability:** ship `SKILL.md` (or AGENTS.md) export for Copilot agents. This requires a strategic decision Microsoft has been reluctant to make. Score is structurally bounded by lock-in incentives, not architectural capability.
- **Audience-safety:** elevate sensitivity labels into a first-class skill-audience primitive. Most of the infrastructure exists; it's a UX/spec lift, not an architectural one.

## Strategic note

For BB1's positioning: Microsoft is the strongest single competitor on freshness + audience-safety + provenance combined, but its 0 on portability is structural (no plausible Microsoft strategy ships a portable agent artifact). That score is the entire reason a portable spec wins as a category vocabulary.
