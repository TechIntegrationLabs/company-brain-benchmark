# The Company Brain Benchmark

> An open methodology for evaluating "company brain" products on the dimensions search benchmarks miss: **freshness, audience-safety, portability, and operational provenance.**
>
> MIT licensed. Disagreement on a score? File an issue. Want your product scored? File an issue.

---

## Why this exists

Most "company brain" products today are evaluated like search products — recall, precision, latency. That benchmark misses the dimensions that actually matter when an AI agent is *doing the work* on top of a company's knowledge.

A company brain is the substrate for reliable AI automation. The benchmark for it should measure:

- **Freshness** — how fast the brain reflects the policy that changed yesterday
- **Audience-safety** — whether operator-only knowledge can ever reach a customer-facing agent
- **Portability** — whether the brain's output is locked to one runtime or travels with the customer
- **Operational provenance** — whether the agent can cite where each fact came from when challenged

This repo defines those four dimensions, scores six current products, and publishes the rationale for every score.

## Quick scoring summary

| | Freshness | Audience-safety | Portability | Provenance | Total /20 |
|---|---|---|---|---|---|
| **BizBrain OS** | 4 | 5 | 4 | 4 | **17** |
| Microsoft Copilot | 4 | 4 | 0 | 4 | 12 |
| Glean | 3 | 3 | 1 | 4 | 11 |
| Hebbia | 2 | 3 | 0 | 5 | 10 |
| Notion AI | 3 | 2 | 0 | 3 | 8 |
| Letta / Mem0 / Zep | 4 | 1 | 2 | 3 | 10 |

See [DIMENSIONS.md](./DIMENSIONS.md) for the rubric. See `scoring/` for per-product rationale.

We deliberately do NOT score on dimensions where BizBrain OS loses — raw enterprise-search recall, distribution to F500, partner ecosystem maturity. Those matter and we're behind. Pick the right tool. If you need to find the document where the policy is written, Glean. If you need an agent to *do the work the way your company does it*, BizBrain OS.

## How scores were derived

Every score in `scoring/` cites either a public engineering blog, public docs, public pricing page, or hands-on testing. We do not score from secondary reporting.

Where a vendor's public docs are ambiguous or marketing-heavy, we mark the score `[UNCERTAIN]` and explain the gap.

## How to contest a score

Open a GitHub issue with:
1. The product
2. The dimension
3. The score we gave
4. The score you think it should be
5. Public evidence (URL, doc, blog post, your own test)

We review weekly. Substantive evidence updates the score and the changelog records who pushed back and why.

## How to add a product

Open an issue with the product name and 1-paragraph architectural summary. We add new products quarterly. We do not promise to score every memory library, vector DB, or workflow framework — only products that publicly position themselves as a "company brain," "knowledge platform," "AI knowledge layer," or equivalent.

## Methodology limitations

This benchmark is opinionated:

- **Bias toward operational use.** We're scoring for "an agent does the work," not "a human searches for the answer." That's a deliberate framing. Search-quality benchmarks are valuable; they live elsewhere.
- **Bias toward portability.** Lock-in is a real cost we surface explicitly. Vendors who don't ship portable artifacts will score 0 on portability and there's no path to a higher score without shipping one.
- **Bias toward production reality.** Open-source memory libraries that require devs to build everything else are scored as libraries, not products. That's a category distinction, not a quality judgment.

## What's NOT in this benchmark

- Raw retrieval quality (covered by RAG benchmarks elsewhere)
- Latency / throughput (relevant but not category-defining)
- Pricing (we list it where public, but we don't score on it)
- Customer count (a popularity contest, not an evaluation)

## Versioning

The benchmark is versioned by date — `v2026.04`. Major rubric changes increment the version. Per-product rescores happen when their products materially change or when public evidence is updated.

## License

MIT. See [LICENSE](./LICENSE).

## Origin

Authored by Will Welsh / BizBrain OS. The methodology was extracted from the requirements list of running multi-tenant company brains in production. We score ourselves first because we wrote the rubric — but the rubric reflects what we built BB1 against, not what makes BB1 win.

If a future product beats us on these dimensions, this benchmark says so honestly.
