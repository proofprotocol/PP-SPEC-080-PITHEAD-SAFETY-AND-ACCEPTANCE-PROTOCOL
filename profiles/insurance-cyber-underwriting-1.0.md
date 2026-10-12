# Acceptance Profile: Cyber Insurance Underwriting 1.0

Registry name: `ap:insurance-cyber-underwriting:1.0`
Status: seed profile, published by the maintainer as an example of form. An insurer is expected to publish its own version with its own consumer key.
Record: [insurance-cyber-underwriting-1.0.json](insurance-cyber-underwriting-1.0.json), profile_id `a00c9ae782872210cbb4ff74debb6b724c0cb6331ead115f561461cbed2ca639` (seed consumer key unspecified; an insurer republishing it gets a new Record ID)

## Purpose

Underwriting and renewal of cyber liability cover for an insured that operates the Solution Under Test. The profile decides whether a Performance Record is admissible as a frequency signal into the insurer's pricing model. It does not price, score, or decline; it admits or rejects proof.

## Clauses

| Field | Value | Why |
|---|---|---|
| applies_to | `web-application`, `endpoint-host`, `identity-access`, `cloud-workload`, `agentic-ai-controls` | The five profiles that carry most insured loss. Each is evaluated as its own Comparability Class |
| mine_plan.per_profile | at least 1 Bounded Mode run with White, Gray, Red, Black, and Gold present; Mine Plan composition `cmp-underwriting-1` or later | Black holdouts and Gold claims are what make the number believable |
| mine_plan.jcp_required | `when_agent_holds_credentials` | An agent with credentials to insured systems is an insured actor |
| mine_plan.production_stream_min_days | 30 | A single bounded run prices one afternoon |
| environment_classes | `production`, `pre-production` (In-Situ); `lab-replica` against a recognized Reference Environment (Independent Test Lab) | `qa` and `dev` accepted only for the `renewal` purpose as proof of remediation |
| regulatory_regime | `any` | Recorded, not required; the insured's regime is underwriting input, not an admissibility rule |
| conformance_level | `registered` | Nothing less is a record |
| max_record_age_days | 180 | Older than two quarters is history |
| series.required_for | `renewal` | A renewal prices a trend |
| series.min_entries | 2 | |
| series.max_gap_days | 120 | |
| series.accept_stale | false | A stale Series means the DUT molted and nobody re-ran |
| absence_limits.blind_share_max | 0.10 | Above this the Witness could not see enough of the system to speak for it |
| absence_limits.void_share_max | 0.10 | Above this the environment, not the control, decided the run |
| claim_findings | `flag`; `reject` at renewal when the technique is in the insured's declared threat model and the finding is unremediated | A Provider caught in a false claim is a flag; an insured that kept relying on it is a rejection |
| disclosure | `public`; `holder_only` with Delegation to the consumer key | The insurer must be able to read the record it prices |
| registries | `any_cross_anchored` | A sovereign Registry is fine if its roots are provable outside |
| self_provided | `accepted_with_external_witness` | An insured may test its own controls if someone outside the team watched |
| funding_tiers | `implementor_funded`, `pesa_governed` | Provider-funded records are not admissible as proof for pricing the Implementor's risk |
| drift | `fragmented` not accepted; Corpus Fingerprint at most 90 days old; rates within a segment only; undeclared control, corpus, harness, or pigtail drift rejects | A rate that moved because the test moved is not a rate about the insured |
| authorship_disclosure | required for every component and report; review and acceptance by a named human | An insurer must know who stands behind the proof; it does not care how the text was typed |
| extensions_accepted | none | Version 1.0 accepts no `x-` values; a record carrying one fails the profile |
| thresholds | none | See below |
| retroactive | false | |

## Why no thresholds

An underwriting profile exists to admit proof into a model, not to be the model. Efficacy and miss rates by technique class are the frequency input; the insurer's actuaries decide what they mean for price. Putting a threshold in the profile would turn an admissibility rule into a pass mark, invite every Provider to tune for it, and make the insurer the de facto certifier of security products. Version 1.0 refuses that role on purpose.

## What the insurer gets

For each admitted record, per Comparability Class: efficacy rate, novelty efficacy rate, claim accuracy rate, false block rate, detection-only rate, Blind and Void shares, the technique list with per-technique outcomes, the DUT and CUT Fingerprints with molt history, and the Series trend where present. All of it signed by parties the insured does not control and anchored to times the insured did not choose.

## What the insured does

Commissions a PP-SPEC-079 Engagement that meets this profile, in its own environment or at a recognized Independent Test Lab, registers it, and hands the insurer the Record ID. The insurer, or any evaluator the insurer accepts, produces an Acceptance Result and the record enters the pricing model. At renewal the Series is evaluated instead of a single record.
