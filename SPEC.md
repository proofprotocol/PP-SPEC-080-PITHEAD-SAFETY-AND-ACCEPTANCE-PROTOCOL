# The Pithead Safety and Acceptance Protocol (PSAP)

*A Proof Protocol specification*

> **Ownership and Attribution Notice**
>
> This specification is authored by **Craig Ellrod** (Nebulonium, Inc., dba HACKERverse) and is published as part of **Proof Protocol**. Copyright (c) 2026 Nebulonium, Inc.
>
> Any use, implementation, derivative, citation, or incorporation of this specification, in whole or in part, MUST attribute **Craig Ellrod, Nebulonium, Inc., and Proof Protocol**. This requirement applies to standards bodies, working groups, consortia, insurers, regulators, and commercial implementations.
>
> This specification is licensed under the Greater Good Commercial License 1.0 (see LICENSE.md); text CC BY-ND 4.0 under its Part S. Original inventor: Craig Thomas Ellrod (ORCID 0009-0004-1058-7666).
>
> **Patents.** Patent terms are in [PATENT-SCHEDULE.md](PATENT-SCHEDULE.md). Claims not listed there are reserved by Craig Ellrod and Nebulonium, Inc. Licensing: 1proofprotocol@gmail.com.
>
> This specification is related to the Proof Economy Prior Art Declaration, DOI [10.5281/zenodo.21379780](https://doi.org/10.5281/zenodo.21379780).

| Field | Value |
|---|---|
| Spec ID | PP-SPEC-080 |
| Version | 0.1.0 (Draft) |
| Date | 2026-10-12 |
| Status | Draft for public record |
| Maintainer | Nebulonium, Inc. (Proof Protocol) |
| Builds on | PP-SPEC-079 v0.1.1 (Coal Mine Protocol), PP-SPEC-077 v0.7.2 (Dead Canary), PP-SPEC-078 v0.2.1 (Jailed Canary), PP-SPEC-004 (ProofRegister API) |

---

## Abstract

The pithead is the top of a mine shaft, where everything that comes up is inspected before anyone relies on it. PP-SPEC-077 and PP-SPEC-078 send the canaries down; PP-SPEC-079 sets the rules of the dig; this specification is the pithead, where the parties who carry the risk decide what they will accept.

PP-SPEC-077, 078, and 079 produce records: Units of Proof, bookings, Performance Records, Performance Series. They say nothing about whether any particular reader should accept one. An insurer underwriting a policy, a regulator supervising a sector, a bank's third-party risk function, a hospital group's procurement office, and an Implementor writing a contract each need to say, in advance and in writing, what a record must satisfy before they will rely on it.

An Acceptance Profile is that statement. It is a short, versioned, registered document that names the Technology Profiles, Mine Plan composition, Environment Classes, Regulatory Regime, Conformance Level, record age, Performance Series requirements, Disclosure Levels, and Registries a consumer requires, and what the consumer does when a record carries a Claim Finding. A Performance Record can be checked against a profile by a machine, a human, or both: it meets the profile or it does not, and if not, the failing clauses are listed. A machine and a human checking the same record against the same profile MUST reach the same result.

A profile never changes a record. It changes only whether a reader takes it. There is one protocol and many readers; this specification gives the readers a common way to say what they need.

## Introduction: Why This Specification Exists

### The problem this family of specifications solves

Nobody can price security risk, because nobody can measure security efficacy. Every control, whether bought, built, or adopted, is described by the party that made it: a datasheet, a demo, a Provider-funded report, a design document, a dashboard of alerts. Implementors choose controls on those descriptions. Insurers underwrite on questionnaires that ask whether controls exist, not whether they work. Regulators supervise against attestations. Each of them is relying on the word of someone with a stake in the answer, and none of them has proof of what a control actually does when an attack arrives.

Agentic AI makes the gap wider and more expensive. An agent acts inside the system with legitimate credentials, decides its next step from text it has just read, and can be persuaded to do what its owner never authorized. The losses it can cause are new, and the controls sold to contain it have no track record. When risk cannot be measured, it is excluded, restricted, or priced as if every control were equally good, which punishes the controls that work and rewards the ones that only claim to.

The Proof Protocol specifications replace description with proof. PP-SPEC-077 measures what a security control did to committed test traffic. PP-SPEC-078 measures whether an agent containment control stopped an agent that tried to break its policy. PP-SPEC-079 makes those measurements independent of whoever built the control, and comparable across controls of any origin. PP-SPEC-080 lets the parties who pay for risk, insurers, regulators, and Implementors, state in advance what proof they will accept. Together they produce records that a person or a machine can verify without trusting the party the record is about.

**This specification's part:** the reader's side, so that the parties who rely on the proof can say what they need and check it the same way every time.

### Why this specification

Nothing can be priced on evidence alone. Evidence is not proof, just as a court does not treat an exhibit as a verdict. Only proof can be priced, and proof that nobody will accept prices nothing. The parties who carry risk, insurers, reinsurers, regulators, auditors, and Implementors, today have nothing admissible to accept, so they fall back on questionnaires and attestations. PP-SPEC-077, 078, and 079 now produce records that can be verified without trusting their producer. What is still missing is a way for each reader to say, in advance and in writing, what a record must satisfy before that reader will rely on it for a decision, and a way to check any record against that statement with the same answer every time.

The obvious way to fill that gap is one specification per vertical: an insurance edition, a healthcare edition, a financial edition, a federal edition. That path is familiar and it fails the same way every time. The editions start identical and drift. Each sector redefines a term to suit itself. The reader who spans sectors, which is every insurer and every large enterprise, loses the one thing the protocol was built to give them: a single record format with a single meaning. And every edition is a document someone else can own.

What differs between verticals is not how a control is tested. A WAF in a hospital is tested the way a WAF in a bank is tested. What differs is what each reader needs before the result counts for their purpose: how much testing, how recent, under what environment rules, with what independence, disclosed to whom. Those are acceptance criteria, and acceptance criteria belong to the party doing the accepting.

It also answers the question every large organization asks before it adopts anything new: is it safe to rely on? A protocol that changes how controls are bought, insured, and supervised will be adopted only if the parties carrying the risk can set their own bar, in writing, before they depend on it, and can check every record against that bar the same way every time. Safety here is not a promise from the protocol's author. It is the reader's own published standard, applied to proof that can be verified without trusting anyone.

So this specification does not describe any vertical. It describes the form of a profile, so that an insurer can publish an insurance profile, a regulator a regulatory one, a sector body a sector one, and an Implementor its own, each pointing at the same protocol specifications by DOI and adding requirements on top, never beneath. The verticals become files in a registry, not forks of a standard.

**Scope.** This specification defines the Acceptance Profile record, how it is published and versioned, how a Performance Record is evaluated against it, and how the result of that evaluation is recorded. It does not define any test, any record of a test, any score, or any mark. It does not produce proof of efficacy, proof of performance, or proof of control.

**Applicability.** Any party that consumes Performance Records for a decision may publish a profile: insurers and reinsurers, regulators and supervisors, auditors, procurement functions, sector consortia, certification bodies, and individual Implementors. Profiles apply to controls of any provenance in any environment, legacy or agentic, because they constrain the record, never the control. A profile is read by people who decide and by machines that evaluate: an underwriter, an auditor, or a procurement officer can apply it by hand, and an agent, API, or underwriting system can apply it automatically, with the same result (3.5, 077 21.14).

**What this is not.** It is not a certification scheme; a profile says what a reader accepts, not what a mark means. It is not a scoring method; PP-SPEC-006 scores, this specification filters. It is not a compliance framework; a profile may require that an Engagement declared a Regulatory Regime, and says nothing about whether the organization complies with that regime.

## 1. Conventions

The key words MUST, MUST NOT, REQUIRED, SHALL, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, MAY, and OPTIONAL are to be interpreted as described in RFC 2119 and RFC 8174.

## 2. Terminology

Terms defined in PP-SPEC-077 Section 2, PP-SPEC-078 Section 2, and PP-SPEC-079 Section 2 have the same meaning here, including Unit of Proof, Performance Record, Performance Series, Comparability Class, Mine Plan, Environment Class, Regulatory Regime, Control Provenance, Conformance Level, Holder, Disclosure Level, Registry, and Extension. The following terms are added:

- **Consumer:** A party that relies on Performance Records for a decision and publishes an Acceptance Profile saying what it requires.
- **Acceptance Profile:** A registered record, under PP-SPEC-077 Section 21, stating the conditions a Performance Record or Performance Series must satisfy to be accepted by a Consumer for a named purpose (Section 4).
- **Purpose:** The decision a profile serves, stated in the profile: underwriting, renewal, procurement, supervisory review, contract remedy, or an `x-` extension.
- **Acceptance Evaluation:** The deterministic comparison, by a machine, a human, or both, of a Performance Record or Series against a profile, producing an Acceptance Result (Section 6).
- **Acceptance Result:** A registered record stating that a record meets a profile, or does not, with every failing clause listed (6.3).
- **Profile Registry:** The registered, versioned list of Acceptance Profiles the maintainer recognizes (Section 7).

### 2.1. Relationship to other specifications

| Specification | What it provides | What this specification adds |
|---|---|---|
| PP-SPEC-079 Coal Mine | The Performance Record and Series, the Comparability Class, Extension Policy (Section 13) | The reader's side: what a record must satisfy to be accepted |
| PP-SPEC-077 Dead Canary | Units of Proof, Section 21 record rules | Profiles and Results are Section 21 records |
| PP-SPEC-078 Jailed Canary | Bookings and verdicts | Profiles may require 078 runs and set verdict thresholds |
| PP-SPEC-006 PES | A score | A profile MAY cite a score threshold; it MUST also state the record-level conditions, since a score alone is not an acceptance criterion |
| PP-SPEC-009 ProofStamp | A mark | A mark's issuer MAY publish its criteria as a profile |
| PP-SPEC-004 ProofRegister | Registry API | Profiles, Results, and the Profile Registry are published there |

## 3. Principles

3.1. **A profile constrains the record, never the control.** No profile may require a particular Provider, Control Provenance, or product. A profile that does is not an Acceptance Profile.

3.2. **A profile adds, never relaxes.** A profile may require more than PP-SPEC-079 requires. It MUST NOT accept a record that 079 would not produce: an Executed run, an unregistered record, a Provider-Run Engagement, a record outside its Comparability Class, or a record whose Registry Receipt does not verify.

3.3. **A profile is published before it is applied.** A Consumer MUST NOT evaluate a record against a profile version that was not registered before the Engagement Manifest of that record was anchored, unless the profile says it applies retroactively and the Holder consents.

3.4. **A profile is a record.** It is hashed, signed, registered, and versioned under PP-SPEC-077 Section 21, so that the Holder of a record can prove which profile version they were measured against.

3.5. **Evaluation is deterministic, by machine or human.** Every clause of a profile MUST be checkable from the Performance Record, its Series, and the Registry, without opinion, so that an agent or API evaluating it and a person evaluating it from the human-readable rendering (077 21.14) reach the same result. A requirement that needs a judgment belongs in the Consumer's own process, after acceptance, not in the profile.

3.6. **Profiles disclose their own authorship.** Every Acceptance Profile carries an Authorship Disclosure under PP-SPEC-077 21.15, referenced from the profile record.

## 4. The Acceptance Profile

4.1. An Acceptance Profile conforms to [schemas/acceptance-profile.schema.json](schemas/acceptance-profile.schema.json) and contains:

| Field | Meaning | Required |
|---|---|---|
| `profile_id` | Record ID under tag `AP-1:profile` (077 21.1) | yes |
| `name`, `version` | Human name and semantic version | yes |
| `consumer` | The publishing party, with public key | yes |
| `purpose` | underwriting, renewal, procurement, supervisory_review, contract_remedy, or `x-` | yes |
| `applies_to` | Technology Profiles (077 Section 17 identifiers, including `x-`) the profile covers | yes |
| `mine_plan` | Required composition and minimum version (079 7.2), per Technology Profile; whether 078 runs are required; minimum Production Stream duration | yes |
| `environment_classes` | Accepted Environment Classes, and whether In-Situ, Independent Test Lab, or either | yes |
| `regulatory_regime` | Required regime set, or `any` | yes |
| `conformance_level` | Minimum run Conformance Level; MUST be `registered` | yes |
| `max_record_age_days` | Maximum age of the Performance Record at evaluation | yes |
| `series` | Whether a Performance Series is required, minimum entries, maximum gap between entries, and whether `stale` series state is accepted | yes |
| `thresholds` | Optional minimums on 077 Section 12 and 078 Section 12 metrics, per Technology Profile, and the Comparability Class they apply within | no |
| `claim_findings` | What a Claim Finding (077 11.6) does: `reject`, `flag`, or `ignore`, optionally per technique class | yes |
| `absence_limits` | Maximum Blind share and Void share (077 14.3) accepted | yes |
| `disclosure` | Accepted Disclosure Levels; whether `holder_only` records are accepted with a Delegation (077 21.10) to the Consumer | yes |
| `registries` | Registries the Consumer recognizes, by identifier, or `any_cross_anchored` | yes |
| `self_provided` | Whether Self-Provided Engagements (079 4.4) are accepted, and if so with what additional separation requirement | yes |
| `funding_tiers` | Accepted PP-SPEC-025 funding tiers | yes |
| `authorship_disclosure` | Whether the record's components and report must carry an Authorship Disclosure (077 21.15), and whether review and acceptance must be by a named human. MUST NOT set a threshold on the AI share of expression | yes |
| `drift` | Whether `fragmented` Series are accepted; maximum Corpus Fingerprint age in days; whether rates across segments are accepted (default no); drift types that, if undeclared in the record, cause rejection | yes |
| `extensions_accepted` | `x-` identifiers the Consumer will accept in records, or none | no |
| `retroactive` | Whether the profile applies to Engagements anchored before it was registered (3.3) | yes |
| `supersedes` | Prior profile version Record ID, if any | no |
| `notes` | Informative text; never evaluated | no |

4.2. A profile MUST name at least one Technology Profile. A profile that names several evaluates each class separately; acceptance is per class unless the profile says all named classes are required together.

4.3. A profile MUST NOT contain a field that names or excludes a Provider, product, or Control Provenance, except that `self_provided` MAY be set to `not_accepted`.

4.4. `thresholds` are optional because the record-level conditions are the acceptance criteria. A Consumer that wants a rate threshold MUST state the Comparability Class it applies within and MUST state how Blind and Void shares are treated when the threshold is computed (077 14.3.3).

## 5. Publication and Versioning

5.1. A profile is published to a Registry under PP-SPEC-004 as a record under PP-SPEC-077 Section 21, with `profile_id` as its Record ID, the Consumer as Holder, and Disclosure Level `public`. A non-public profile is a private contract term, not an Acceptance Profile.

5.2. Versions follow semantic versioning. A change that makes any accepted record unacceptable is a major version. A profile version is immutable once registered; corrections are new versions with `supersedes` set.

5.3. A Consumer MAY withdraw a profile by Revocation (077 21.6). Records already accepted under it remain accepted; new evaluations against it are not permitted.

5.4. A profile SHOULD be published at least 90 days before it is first applied to new Engagements, so that Holders can commission Engagements that meet it.

## 6. Acceptance Evaluation

6.1. An evaluation takes one Performance Record, or one Performance Series, and one profile version, and checks every clause in Section 4 against the record, its Series, and the Registry. The evaluator MUST verify the record's Registry Receipt and Record ID (077 21.2.2, 21.5.2) before evaluating anything else; a record that fails verification fails the profile.

6.2. Evaluation order: receipt and Record ID; Conformance Level; undeclared drift; Comparability Class membership (Technology Profile, Mine Plan composition and version, Environment Class, Parity Declaration or Reference Environment, Regulatory Regime); Engagement Mode and Self-Provided rule; funding tier; record age and Series requirements; absence limits; Claim Findings rule; disclosure and Delegation; extensions; thresholds last. The order exists so that a threshold is never reported as the reason a record failed when the record was not comparable in the first place.

6.3. **Acceptance Result.** The evaluator MUST produce an Acceptance Result record, under tag `AP-1:result`, containing: the Performance Record or Series Record ID; the profile Record ID and version; the evaluation time and Time Anchor pulse; `meets: true | false`; for a failing record, every failing clause by field name with the record's value and the profile's requirement; the evaluator's identity and signature; and the Registry Receipt once registered.

6.4. The Acceptance Result is registered and its Record ID returned to the Holder. The Holder MAY attach the Result to the Performance Record's Signature Envelope as an endorsement (077 21.4.2). A Result is never written into the Performance Record itself.

6.5. An evaluator MAY be the Consumer, the Holder, an Independent Test Lab, an agent, an API, or a person; the Result says who and whether the evaluation was by machine, human, or both (`evaluated_by`). The reference evaluator in the ProofSwarm reference implementation is the conformance target for evaluators: identical Results on identical inputs.

6.6. A Result that reports `meets: true` on a record that fails any Section 4 clause is a defective Result, and the evaluator's Results MAY be revoked by the Consumer under 077 21.6.

## 7. The Profile Registry

7.1. The maintainer keeps a Profile Registry: a registered Bundle (077 21.7) of the profile Record IDs the maintainer recognizes, with name, version, Consumer, purpose, and status (`current`, `superseded`, `withdrawn`).

7.2. Any Consumer may publish a profile without recognition; recognition means only that the maintainer has checked the profile against Section 3 and Section 4 and lists it. A recognized profile MAY be cited by its registry name, for example `ap:insurance-cyber-underwriting:1.0`.

7.3. The maintainer publishes seed profiles for the purposes it expects to be common. Seed profiles are examples of form; a Consumer is expected to publish its own.

## 8. Worked Profile: Cyber Insurance Underwriting

The first seed profile is given in full in [profiles/insurance-cyber-underwriting-1.0.md](profiles/insurance-cyber-underwriting-1.0.md) and as a record in [profiles/insurance-cyber-underwriting-1.0.json](profiles/insurance-cyber-underwriting-1.0.json). In summary:

- **Purpose:** underwriting and renewal of cyber liability cover for an insured operating the SUT.
- **Applies to:** Web Application, Endpoint and Host, Identity and Access, Cloud Workload, and Agentic AI Controls profiles, each evaluated as its own class.
- **Mine Plan:** at least one Bounded Mode run per applicable profile with all five colors present; 078 runs required where any agent holds credentials to insured systems; a Production Stream commitment of at least 30 days for `production` or `pre-production` In-Situ.
- **Environment:** In-Situ in `production` or `pre-production`, or Independent Test Lab against a Reference Environment the insurer recognizes. `qa` and `dev` not accepted for underwriting; accepted for renewal as proof of remediation.
- **Regime:** any; recorded.
- **Conformance Level:** Registered.
- **Age and Series:** record no older than 180 days at binding; a Series with at least two entries no more than 120 days apart for renewal; `stale` not accepted.
- **Absence limits:** Blind share at most 10 percent, Void share at most 10 percent, per run.
- **Claim Findings:** `flag`; an unremediated Claim Finding on a technique in the insured's declared threat model is `reject` at renewal.
- **Disclosure:** `public` or `holder_only` with a Delegation to the insurer.
- **Registries:** any cross-anchored to a public Registry.
- **Self-Provided:** accepted with an external Proof Witness.
- **Funding:** Implementor-Funded or PESA-Governed; Provider-Funded not accepted for underwriting.
- **Authorship:** disclosure required for every component and report; review and acceptance by a named human required; no threshold on AI share.
- **Drift:** `fragmented` not accepted; Corpus Fingerprint no older than 90 days at the record's last run; rates only within a segment; any undeclared control, corpus, harness, or pigtail drift rejects the record.
- **Thresholds:** none in version 1.0. The insurer's pricing model consumes the rates; the profile only decides whether a record is admissible to it.

The profile deliberately sets no efficacy threshold. An underwriting profile exists to admit proof into a pricing model, not to replace the model. The frequency signal is the efficacy and miss rates by technique class; the severity signal comes from elsewhere; the profile's job is to make sure the frequency signal is real, recent, comparable, and independently produced.

## 9. Integration Points

PP-SPEC-079 Section 12 applies. This specification adds:

| ID | Integration Point | What plugs in | MUST do | MUST emit |
|---|---|---|---|---|
| **IP-A1** | Profile Publisher | Consumer tooling, GRC platforms | Produce a profile conforming to Section 4; register it; version it | Acceptance Profile record |
| **IP-A2** | Evaluator | Underwriting systems, procurement tools, audit platforms, the reference evaluator | Verify the record; evaluate in the Section 6.2 order; register the Result | Acceptance Result record |
| **IP-A3** | Profile Registry Client | Any | Resolve a profile name to a Record ID and version; check status | Resolution record |

An Evaluator MUST NOT be the Provider of any control in the evaluated record. Conformance to IP-A2 is established only by identical Results to the reference evaluator on the published vectors.

## 10. Security Considerations

- **Profile shopping.** A Holder could evaluate a record against the weakest available profile. Mitigated by purpose: a Result names the profile, and a Consumer accepts only Results against its own profile versions.
- **Retroactive tightening.** A Consumer could change a profile after Engagements were commissioned against it. Mitigated by 3.3, 5.2 immutability, and the anchor comparison in 6.1.
- **Threshold as a back door.** A profile could use a threshold to exclude a Provider indirectly. Mitigated by 3.1, 4.3, and the requirement that thresholds apply within a Comparability Class to all records alike.
- **Evaluator capture.** A Provider-run evaluator could issue favorable Results. Mitigated by the Section 9 separation rule and 6.6 revocation.
- **Stale profiles.** A profile that never changes will accept records the Consumer no longer wants. Mitigated by versioning and the Profile Registry status.

## 11. Extension Policy

PP-SPEC-079 Section 13 applies. `purpose`, Technology Profile identifiers, Regulatory Regime values, and profile fields under `extensions.<consumer>` may be extended under `x-`. The Section 4 required fields, the Section 6.2 evaluation order, and the Section 3 principles are not extensible.

## 12. Reserved

Profiles for supervisory review by financial and healthcare regulators, profile composition (a profile that requires another profile), and Consumer federations sharing a profile are reserved for future revisions by the maintainer.

## 13. Interpretation

Nebulonium, Inc., as maintainer of Proof Protocol, reserves final interpretive discretion over this specification, over recognition of profiles, and over conformance claims made under it.

## Revision History

| Version | Date | Notes |
|---|---|---|
| 0.1.0 | 2026-10-12 | Initial draft. Titled the Pithead Safety and Acceptance Protocol; adoption safety for risk-bearing organizations stated in the Introduction. Shared family problem statement; Introduction opens from the reader's problem. 3.6 and `authorship_disclosure` field (077 21.15). Profiles and Results usable by machines and humans with the same result (3.5, 6.5, 077 21.14). Acceptance Profile record, principles (constrains the record never the control; adds never relaxes; published before applied; deterministic evaluation by machine or human), publication and versioning, Acceptance Evaluation and Result, Profile Registry, worked cyber insurance underwriting profile, IP-A1 to IP-A3. Builds on PP-SPEC-079 v0.1.1. |
