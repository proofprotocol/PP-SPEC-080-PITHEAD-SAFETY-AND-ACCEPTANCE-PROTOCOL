# Changelog

## 0.1.2 (2026-10-23)
- 2.1: PP-SPEC-081 Reproof row.
- 4.1, 4.5: required `reproof` field; a Repeat Run never satisfies it; `none` must be stated explicitly.
- 6.2: reproof evaluated after extensions, before thresholds.
- Section 8 and profiles/: seed insurance underwriting profile 2.0 requires reproof; supersedes 1.0.
- schemas/acceptance-profile.schema.json: `reproof`.
- License: Proof Protocol License 1.1. Specification text is CC BY 4.0 from this version (LICENSE-CC-BY-4.0.md), which grants no patent rights; patents only under LICENSE.md Part A2 and PATENT-SCHEDULE.md. Earlier versions remain Apache-2.0 (Part A6).

## 2026-10-20 (licensor)

- Licensor, copyright holder, maintainer and author changed from Nebulonium, Inc. (dba HACKERverse) to Craig Thomas Ellrod. Contact: CraigEllrod@gmail.com. Historical statements of what HACKERverse published and when are unchanged.
- LICENSE.md: ProofStamp named as a Mark; new C9 makes ProofStamp issuance exclusive to the Licensor and excludes it from any transfer to PESA. ETHICS.md section 4 states the same.

## 2026-10-19

- Adopted the Proof Protocol License 1.0 (LICENSE.md). Specifications: Apache-2.0. Software: proprietary.
- Added ETHICS.md (Proof Economy Code of Ethics).
- All prior versions of the specifications are relicensed under Apache-2.0 (see NOTICE.md).

## 0.1.1 (2026-10-13)
- Section 13: maintainer responsible for editorial text only; conformance determined from the records, not decided by the maintainer
- CONTRIBUTING.md updated to match
- Proof, not evidence: wherever the text meant what the protocol produces, relies on, accepts, or prices, "evidence" is now "proof". Evidence remains the word for inputs inside a proof record (liveness, cause, differential, verification evidence). Evidence is not proof; proof contains evidence.

## 0.1.0 (2026-10-12)
- Follows PP-SPEC-079 role and environment terms: Implementor, Provider, `dev`, Independent Test Lab, `implementor_funded`; seed profile Record ID recomputed
- FUNDING.md funding disclosure ([FUNDED] Yes or No, [FUNDED BY] name and URL per funder); Proof Economy Code of Ethics applies
- Titled the Pithead Safety and Acceptance Protocol; adoption safety for risk-bearing organizations stated in the Introduction and README
- Initial draft: Acceptance Profile record and schema; principles (constrains the record never the control, adds never relaxes, published before applied, mechanical evaluation); publication and versioning; Acceptance Evaluation order and Acceptance Result record; Profile Registry; IP-A1 to IP-A3
- Seed profile: Cyber Insurance Underwriting 1.0, with no thresholds by design
