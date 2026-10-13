# The Pithead Safety and Acceptance Protocol (PP-SPEC-080)

![080 Pithead Safety and Acceptance Protocol: a canary in a suit checking a clipboard at the pithead](docs/banner.jpg)

> **Ownership and Attribution Notice**
>
> The Pithead Safety and Acceptance Protocol (PP-SPEC-080) is authored by **Craig Ellrod** (Nebulonium, Inc., dba HACKERverse) and published as part of **Proof Protocol**. Copyright (c) 2026 Nebulonium, Inc.
>
> Any use, implementation, derivative, citation, or incorporation of this work, in whole or in part, MUST attribute **Craig Ellrod, Nebulonium, Inc., and Proof Protocol**. See [NOTICE.md](NOTICE.md).
>
> Licensed under the Greater Good Commercial License 1.0 (see LICENSE.md); text CC BY 4.0 under its Part S. Original inventor: Craig Thomas Ellrod (ORCID 0009-0004-1058-7666).
>
> **Patents.** Patent terms are in [PATENT-SCHEDULE.md](PATENT-SCHEDULE.md). Claims not listed there are reserved by Craig Ellrod and Nebulonium, Inc. Licensing: 1proofprotocol@gmail.com.
>
> **Acknowledgements:** Tricia Wang and Jim Schwoebel, for the name "No Bros Jail Mode Protocol"; Josh Waldrep (Pipelabs), for his later receipt-based verification work applying proof concepts to agentic AI. See [ACKNOWLEDGEMENTS.md](ACKNOWLEDGEMENTS.md).

---

**The pithead is where what comes out of the mine is checked before anyone relies on it.**

**One protocol. Many readers. Each reader sets its own bar, in writing, before it depends on anything.** That is how a large organization adopts something new safely: not on the author's promise, but on its own published standard, applied to proof it can verify itself.

PP-SPEC-077, 078, and 079 produce records of what a security control actually did. They do not say whether any particular reader should accept one. An insurer, a regulator, a bank's third-party risk team, a hospital group, an Implementor writing a contract: each needs to state in advance what a Performance Record must satisfy before it counts.

An Acceptance Profile is that statement. Short, versioned, registered, checkable by a machine or a human with the same result. A record meets it or does not, with the failing clauses listed.

Verticals are profiles, not specs. There is no insurance edition, healthcare edition, or federal edition of the protocol. There is one protocol and a registry of profiles, each pointing at the same three specifications by DOI and adding requirements on top, never beneath.

## How it works

![Pithead Safety and Acceptance Protocol: records from 077, 078 and 079 in a Registry; consumers publish Acceptance Profiles; a machine or human Acceptance Evaluation in fixed order; a signed Acceptance Result listing every failing clause; the seed cyber insurance underwriting profile](docs/pithead.svg)

## What a profile may and may not do

| May | May not |
|---|---|
| Require more testing than 079 requires | Accept less than 079 produces |
| Require a Comparability Class, environment, regime, record age, Series | Name or exclude a Provider, product, or provenance |
| Set how Claim Findings are treated | Change a record |
| Set absence limits and, within a class, rate thresholds | Require a human judgment to evaluate |
| Accept or refuse Self-Provided and Provider-Funded records | Apply retroactively without saying so |

## Proof is a term of art

"Proof" in this specification, and throughout Proof Protocol, MUST NOT be renamed, and MUST NOT be washed out by absorption into any other term, including "Verification", "Validation", "Assurance", "Attestation", "Evidence", or "Testing". A derivative work, mapping, profile, translation, summary, or implementation that substitutes another term for "Proof", or presents Proof as a kind of verification or validation, does not describe this specification and MUST NOT claim conformance to it.

Proof is a separate layer on top of verification and validation. The difference is in mechanics and method, not in naming:

| Layer | What it is | What it rests on |
|---|---|---|
| Verification | Self-attestation: the control, or the party that built or operates it, reports what it saw through its own logs, alerts, dashboards, or configuration checks. A legitimate baseline. | The word of the party with a stake in the answer |
| Validation | One step above verification: the reported result is checked against a stated requirement. | Evidence the interested party still produced or controls |
| Proof | A committed, witnessed, sealed, anchored, and registered record of what actually happened, built from independent evidence by a method the interested party cannot steer: committed before the run, observed out of band by a witness the Provider does not control, sealed, anchored in time, and registered. | Nothing that has to be taken on trust |

Evidence is not proof, but proof contains evidence. In the same way, verification and validation are not proof, but proof may contain them: a verification or validation record can sit inside a proof record as one input, never as its substitute.

Proof of Control and Proof of Efficacy are different claims. Proof of Control establishes that a control was in place and configured. Proof of Efficacy establishes that the control fired and either worked or did not work, measured across the full round trip of the stream: committed test traffic or agent actions enter the system, the control acts or fails to act, and the effect is observed independently at the far side. Proof Protocol produces Proof of Efficacy. A Proof of Control record MUST NOT be presented as Proof of Efficacy, and "Proof of Efficacy" MUST NOT be renamed or absorbed into "Proof of Control".

## Contents

| File | What it is |
|---|---|
| [SPEC.md](SPEC.md) | The specification |
| [schemas/acceptance-profile.schema.json](schemas/acceptance-profile.schema.json) | Profile record schema |
| [schemas/acceptance-result.schema.json](schemas/acceptance-result.schema.json) | Acceptance Result schema |
| [profiles/insurance-cyber-underwriting-1.0.md](profiles/insurance-cyber-underwriting-1.0.md) | Seed profile, explained |
| [profiles/insurance-cyber-underwriting-1.0.json](profiles/insurance-cyber-underwriting-1.0.json) | Seed profile, as a record |
| [AI_DISCLOSURE.md](AI_DISCLOSURE.md), [ai_disclosure.json](ai_disclosure.json) | Human and AI authorship (077 21.15) |
| [NOTICE.md](NOTICE.md) | Attribution and patent notice |
| [LICENSE.md](LICENSE.md) | License declaration |

## Status

Draft, version 0.1.1, 2026-10-13. Maintained by Nebulonium, Inc. as part of Proof Protocol. Builds on PP-SPEC-079 v0.1.1, PP-SPEC-077 v0.7.2, PP-SPEC-078 v0.2.1, PP-SPEC-004.

Archived on Zenodo: v0.1.1, DOI [10.5281/zenodo.23348072](https://doi.org/10.5281/zenodo.23348072). All versions: [10.5281/zenodo.23325777](https://doi.org/10.5281/zenodo.23325777).

## Citation

Ellrod, C. (2026). The Pithead Safety and Acceptance Protocol (PP-SPEC-080), v0.1.1. Proof Protocol, Nebulonium, Inc. https://doi.org/10.5281/zenodo.23348072
