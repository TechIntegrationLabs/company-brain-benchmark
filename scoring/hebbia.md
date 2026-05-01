# Hebbia

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Freshness | 2 | Workspace-scoped document analysis. Documents are uploaded or connector-ingested per project. Strong on deep static analysis; weaker on continuous live-comms ingestion. Updates require re-running the matrix or re-uploading. |
| Audience-safety | 3 | Enterprise SOC2 / SSO / SCIM controls. Per-workspace permissions and information barriers for the finance/legal customer base. No first-class skill-audience model because the output is analysis, not a skill artifact. |
| Portability | 0 | Output is Matrix grids (rows = documents, columns = questions) inside Hebbia's UI. No portable skill-file format. API exists for embedding the analysis surface, but the analysis itself is product-bound. |
| Operational provenance | 5 | Best-in-class. Cited cells with direct page/line links. Iterative Source Decomposition (ISD) produces auditable reasoning trees over source documents. This is Hebbia's strongest moat. |
| **Total** | **10 / 20** | |

## Architecture summary

Hebbia's Matrix product runs an "agent swarm" using ISD (Iterative Source Decomposition) — an orchestrator decomposes a question into sub-questions, dispatches subagents over selected documents, and reassembles answers with cell-level provenance. Designed for analyst workflows in finance and legal.

Series B of $130M at ~$700M valuation (mid-2024). Heavy penetration in asset managers (BlackRock, KKR, Carlyle reportedly use it) and large-firm legal.

## What it does best

- Deep document analysis at scale (claims of 1B pages processed)
- Cell-level cited provenance — auditable for compliance review
- Vertical excellence in finance / legal where the document corpus IS the operational reality

## What it doesn't do

- Continuously ingest from live comms (Slack, email, meetings) as primary signal
- Emit anything an external agent runtime can load and act on
- Operate as a generalized "company brain" outside finance/legal vertical
- Brain-per-managed-client architecture
- Auto-evolving schema

## Sources

- [Hebbia $130M raise (VentureBeat)](https://venturebeat.com/ai/hebbia-nets-130m-to-build-the-go-to-ai-platform-for-knowledge-retrieval)
- [Hebbia Sacra revenue profile](https://sacra.com/c/hebbia/)
- [Hebbia ISD architecture deep-dive (Cuckoo)](https://cuckoo.network/blog/2025/06/07/hebbia)

## What would move their score

- **Portability:** ship an export format that lets the Matrix output run elsewhere — even an MCP-server interface would move the score from 0 to 2.
- **Freshness:** wire continuous ingestion of live comms as primary signal, not just document upload.

## Strategic note

Hebbia is the closest in spirit to "structured executable knowledge from source documents." The product is excellent in its vertical. The benchmark gap is that document analysis ≠ live operational memory. Hebbia is what to use when the question is "what does this 200-page deal doc tell me." It is not what to use when the question is "what's the current refund policy and how do agents handle exceptions in real time."
