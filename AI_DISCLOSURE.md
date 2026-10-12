# AI Disclosure

*How this specification was made, and by whom. Required by PP-SPEC-077 Section 21.15.*

## Summary

PP-SPEC-080, the Pithead Safety and Acceptance Protocol, answers a question Craig Ellrod asked: whether each vertical (insurance, healthcare, financial, federal) needs its own specification. The answer, one specification of Acceptance Profiles with verticals as profiles, was proposed by Claude, an AI assistant made by Anthropic, and accepted by Craig Ellrod. The use case it serves, that the protocol can let insurers underwrite agentic AI again, is his. The words are Claude's, drafted under his direction; every section is subject to his review before a release is tagged.

## Ratio

| Dimension | Human | AI |
|---|---|---|
| Conception and every normative decision | 60% | 40% |
| Design details and naming | 20% | 80% (The profile mechanism, its principles, field list, evaluation order, and the insurance seed profile were proposed by Claude in answer to the human's question about per-vertical specs, and accepted ("ok do it")) |
| Words, code, and schemas as written | 3% | 97% |
| Review, direction, acceptance, decision to publish | 100% | 0% |

Method: self-estimated. Shares drafted by the AI from its itemized record of what it proposed and what the author directed, for the author to confirm or correct before release. MAY be re-measured with a tool such as ProofJack.com.

Machine-readable form: [ai_disclosure.json](ai_disclosure.json), conforming to PP-SPEC-077 Section 21.15. The two forms agree; if they ever differ, the JSON is wrong and must be corrected.

## This version (0.1.0, 2026-10-12)

**Human:**
- The question whether each vertical needs its own spec
- The insurance underwriting use case and the claim that the protocol holds the keys to underwriting agentic AI
- Machine and human evaluation requirement
- Drift and authorship requirements carried into profiles
- Review and acceptance

**AI:**
- The answer: one spec of profiles, verticals as profiles
- Text as written
- Principles, field table, evaluation order, Result record, Profile Registry
- Seed profile clauses and the no-threshold rationale

**Proposed by the AI, pending the author's explicit acceptance:**
- Every seed profile value (180 days, 10 percent absence caps, 90-day corpus age, funding tiers)

AI systems: Anthropic Claude (Fable 5.1, Opus 5.5).

## What the AI did not do

- Decide that the protocol should serve insurers, or that it must be usable by machines and humans, or that drift and authorship must be carried into profiles. Those were Craig Ellrod's requirements.
- Publish anything. Publication is the author's decision.
