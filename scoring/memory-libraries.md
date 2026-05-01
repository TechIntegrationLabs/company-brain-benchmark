# Letta + Mem0 + Zep (memory libraries, scored as a category)

> These are not directly comparable to BizBrain OS, Glean, Notion, Copilot, or Hebbia — they are *libraries* developers use to build memory-aware agents. We score them as a category because they share the same architectural posture and gaps.

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Freshness | 4 | Real-time agent memory by design — these are state stores for stateful agents. Letta has tiered memory (core/recall/archival) with self-edit semantics. Zep/Graphiti is bitemporal with valid-from/ingestion-time. Mem0 has decay + relevance scoring. Where the developer wires ingestion correctly, freshness is excellent. |
| Audience-safety | 1 | Per-agent / per-user scoping primitives (Mem0's `user_id`/`agent_id`/`app_id`/`run_id`; Letta's per-agent rows; Zep's user/group). Audience-safety in the operator-vs-customer-safe sense is not a primitive any of them ship; it's a thing the developer would have to build on top. |
| Portability | 2 | Output is "agent state in a database the library manages" — there's no `SKILL.md` emission story. Some library-level export but no cross-runtime artifact format. Zep / Mem0 / Letta agents are themselves portable across LLM providers, but their *memory* is locked to their own runtime. |
| Operational provenance | 3 | Each library tracks message provenance internally; some surface citations to the agent in retrieval. None natively cite to external sources (email thread, Slack channel, meeting) the way an enterprise brain needs to. |
| **Total** | **10 / 20** | |

## Architecture summaries

**Letta** (formerly MemGPT). Stateful agents with explicit memory hierarchy: core memory blocks always in context, recall memory (raw conversation), archival memory (vector + graph). Agent self-edits memory via tools. Open-source + managed cloud.

**Mem0.** Universal memory SDK. Hybrid vector + graph. Workspace/project/user namespaces. Token-efficient compression. $24M Series A in Oct 2025 led by YC + Basis Set + Peak XV. 50K+ developers. AWS Bedrock Agent SDK exclusive memory partner.

**Zep / Graphiti.** Temporal knowledge graph for agents. Bitemporal: every edge has both event-time and ingestion-time. Hybrid retrieval (semantic + BM25 + graph traversal). 71.2% on LongMemEval (vs Mem0's 49% on the same benchmark with GPT-4o). Open-source Graphiti library + commercial Zep cloud. YC W24.

## What they do best

- Give developers programmable, transparent agent memory
- Solve the "agent doesn't remember the previous conversation" problem at the library layer
- Let any LLM provider be the brain; the memory is portable across model swaps

## What they don't do

- Productized "company brain" with ingestion connectors, schema evolution, and audience scoping out of the box
- Emit portable skill-file artifacts — they store memory, they don't compile it into agent-loadable instructions
- Multi-tenant brain-per-customer with first-class operator/customer separation
- Continuous ingestion of company comms (Gmail, Slack, WhatsApp, Drive, meetings) — those have to be wired by the developer

## Sources

- [Letta v1 agent loop](https://www.letta.com/blog/letta-v1-agent)
- [Letta — Agent Memory](https://www.letta.com/blog/agent-memory)
- [Mem0 $24M Series A (TechCrunch)](https://techcrunch.com/2025/10/28/mem0-raises-24m-from-yc-peak-xv-and-basis-set-to-build-the-memory-layer-for-ai-apps/)
- [Mem0 production paper (arXiv 2504.19413)](https://arxiv.org/abs/2504.19413)
- [Zep / Graphiti paper (arXiv 2501.13956)](https://arxiv.org/abs/2501.13956)
- [Graphiti GitHub](https://github.com/getzep/graphiti)

## What would move their score

These products would either need to evolve into productized brains (out of scope for what they currently sell) or remain as the underlying infrastructure that products like BB1 sit on top of. Both are valid roads.

## Strategic note

For BB1's positioning: these are not competitors. They're potential infrastructure dependencies or peer infrastructure layers. A future BizBrain OS could plausibly use Mem0 or Graphiti underneath — the brain-compiler layer is independent of the memory storage substrate.
