# The Four Dimensions

> The complete rubric. Each dimension scored 0-5 with concrete criteria.

---

## 1. Freshness

**Definition:** When the company's operational reality changes (a policy update in Slack, a verbal decision in a meeting, a new SOP added to Drive), how long until the brain reflects it in what an agent loads?

**Why it matters:** Stale knowledge causes the most expensive failure mode in production — the agent confidently doing the wrong thing. A refund policy that changed in February but is still being followed in April is worse than no automation at all.

| Score | Criteria |
|-------|----------|
| **0** | Brain is rebuilt manually. Updates require explicit re-indexing or human curation. |
| **1** | Scheduled re-ingestion at intervals (daily / weekly). Source changes are not detected; they're scanned. |
| **2** | Webhook or polling-based ingestion. New documents picked up within hours but no semantic understanding of "this changed the policy." |
| **3** | Continuous ingestion across most relevant sources (email, docs, chat). Updates within minutes-to-hours. Some understanding of "change detected" but no automatic skill regeneration. |
| **4** | Continuous ingestion across all comms surfaces (email, Slack, WhatsApp, Drive, meetings). Skill artifacts auto-regenerate when source provenance changes. Freshness lease enforces re-validation. |
| **5** | Continuous + bitemporal. Every fact has `valid_from` / `valid_to`. "What did we believe on March 1?" is a queryable thing. Skills carry their own validity windows and refuse to load if expired without acknowledgment. |

---

## 2. Audience-safety

**Definition:** Can the brain enforce that operator-only knowledge (pricing strategy, risk scores, M&A notes, internal post-mortems) cannot ever load into a customer-facing agent session?

**Why it matters:** Required for regulated industries (legal, healthcare, finance), managed-services / agency operators (one operator runs brains for many customers), and any business with material asymmetry between what the operator knows and what the customer sees.

Document ACLs are insufficient — they protect *retrieval* of the source document, but they don't prevent the agent from paraphrasing internal context into a customer-facing response.

| Score | Criteria |
|-------|----------|
| **0** | No audience model. All ingested data is equally retrievable. Operator-only knowledge has to be physically separated into a different system. |
| **1** | Document/page-level ACLs. Permission inheritance from source systems. Vulnerable to paraphrase leakage at the agent layer. |
| **2** | Document ACLs + role-based query filtering at retrieval time. Still vulnerable to paraphrase. |
| **3** | Tagging or classification at ingestion. Some runtime filtering. No formal audience boundary in the artifact format itself. |
| **4** | Audience as a first-class metadata field on every fact / skill. Runtime guard refuses to load operator-only artifacts in customer-facing sessions. Hook-gated at write time. |
| **5** | First-class audience primitive + cryptographic signing of audience scope + audit trail proves operator-only data has never crossed the boundary. Suitable for regulated-industry compliance review. |

---

## 3. Portability

**Definition:** Can the same brain output run on Claude Code, Cursor, Codex, OpenAI Agents SDK, Lindy, Devin, or whichever agent runtime the customer chooses tomorrow? Or is the output locked to one vendor's UI?

**Why it matters:** Vendor lock-in is the buyer's #1 fear in 2026. Buyers actively de-rank products whose output cannot leave the vendor. Portable skill-file artifacts (Anthropic Skills, AGENTS.md) are the answer.

| Score | Criteria |
|-------|----------|
| **0** | All output is locked to the vendor's runtime, UI, or API. The customer's knowledge is the vendor's hostage. |
| **1** | Some export of raw underlying data (CSV, JSON dump). No structured artifact that an external agent can load and act on. |
| **2** | Vendor-specific instruction format (e.g., `.cursorrules`, custom GPT instructions, vendor-prompted memory). Works only inside that ecosystem. |
| **3** | Output is plain markdown or structured text. Manually reusable but no conventions for tools, audience, or provenance metadata. |
| **4** | Output conforms to a published cross-vendor standard (Anthropic `SKILL.md`, AGENTS.md). Loadable by any compliant runtime. |
| **5** | Output conforms to standards + extends them safely with audience / provenance / validity metadata that ignored-by-default for non-aware runtimes. Strict superset = no lock-in penalty for adopting the extension. |

---

## 4. Operational provenance

**Definition:** When the agent cites or acts on a fact, can it point to the email thread, Slack channel, meeting transcript, or document that produced that fact?

**Why it matters:** Required to debug hallucinations, re-validate when sources change, and pass an audit. Regulated industries demand it. Sophisticated buyers ask for it within the first 30 minutes of a serious evaluation.

| Score | Criteria |
|-------|----------|
| **0** | No provenance. Agent answers as if from authority. No way to trace a claim back to source. |
| **1** | Some provenance at retrieval (the document the chunk came from), but lost when the agent paraphrases. |
| **2** | Provenance preserved through paraphrase via citation conventions. Coverage is uneven. |
| **3** | Provenance is mandatory in retrieval, citations are inline. Covers all document types but weak on chat / meetings. |
| **4** | Provenance covers all source types (email, chat, docs, meetings) and survives skill emission. Each skill artifact lists its source pointers. |
| **5** | Provenance covers all sources + cryptographic proof that the cited source produced the cited fact. Suitable for legal / compliance defense. |

---

## Notes on scoring

- A 5 is rare and intentional. It represents the kind of property regulated industries audit against, not just claim.
- A 0 is also rare. Most products score 1-3 across most dimensions.
- We score products, not roadmaps. "Coming in Q3" doesn't move the score.
- We re-score quarterly or when a vendor publishes a material architectural change.
