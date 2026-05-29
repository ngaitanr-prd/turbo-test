# PRD Reconciliation: Gaps Against Source Documents
**PRD:** prd.md (Canonical Data Layer and Order Entry Form)
**Sources:** problem-statement.md, problem-space-analysis.md
**Date:** 2026-05-27
**Resolved:** 2026-05-27

---

## Source 1: problem-statement.md

**1. Scope boundary / discipline constraint not reflected**
> The problem statement warns against scope creep into tribal knowledge, prior auth, and self-pay while "already in there."

**Resolution: DISMISSED** — PM concern, not a product requirement. §5 Non-Goals explicitly lists all deferred capabilities; the discipline is enforced by the non-goals section, not a separate principle statement.

---

**2. Auditability as an explicit requirement**
> The problem statement frames the core failure as data that is not "auditable."

**Resolution: DISMISSED** — NFR-2 (Basic auditability) requires that every submitted Order is associated with the employee who created it and the creation timestamp, and that this record cannot be modified after submission. Field-level audit log is explicitly deferred in NFR-2's out-of-scope note.

---

**3. "Same inputs, same output" not formalized as a requirement**
> No FR explicitly requires deterministic end-to-end order output — submitted values could silently change if catalog data changes later.

**Resolution: CONVERTED TO OQ-6** — Added to §8: *"When an Order is submitted, are the computed values (unit price, Billable Amount, Margin) locked as a point-in-time snapshot, or do they remain linked to live catalog and fee schedule data?"* Required before data model is designed.

---

**4. Baseline capture stated as prerequisite — not surfaced as an action item**
> The PRD's §7 baseline note was advisory and risked being overlooked.

**Resolution: APPLIED TO §7** — Elevated from a soft note to a named pre-launch gate with a three-row table specifying what to capture (SM-1, SM-2, SM-3), over what period, and from what source.

---

**5. Order lead time metric scoping**
> SM-2 measures "clinic order received to order placed with vendor" but the system has no FR capturing a "clinic order received" timestamp.

**Resolution: CONVERTED TO OQ-7** — Added to §8: *"Does the employee enter an Order immediately upon receiving the clinic's order, or is there a meaningful lag? If there is a lag, a separate 'date received from clinic' field is needed to measure SM-2 accurately."* Required before metrics can be fully instrumented.

---

## Source 2: problem-space-analysis.md

**1. Compliance risk dimensions not reflected in requirements**
> Billing errors can trigger audits or recoupment demands; no data integrity requirement addresses this.

**Resolution: DISMISSED** — Subsumed by OQ-6 (submitted order value locking). NFR-2 covers record immutability at submission. Further compliance hardening (field-level validation tied to billing compliance) is a solution design decision.

---

**2. Access controls on sensitive patient/billing data**
> The analysis flags "no access controls on sensitive patient/billing data" as a compliance-medium risk; the PRD has no authentication requirement.

**Resolution: DISMISSED** — NFR-1 already requires that the system restricts access to patient and billing data to authorized internal staff only, and states that the access model is defined at deployment. This is the correct abstraction level for a PRD; the mechanism is a solution design decision.

---

**3. "Design the data model alongside the first form, not before it"**
> The analysis documents this as a mitigation for over-engineering risk; the PRD did not reflect it.

**Resolution: APPLIED TO §9** — Added as a named assumption in the Assumptions Index: the data model is designed in parallel with the Order Entry Form, not as a prior sequential phase, with rationale.

---

**4. "Scope the data model to exactly what the first order entry form needs — nothing more"**
> The PRD includes the HCPCS approval-required flag and MSRP as scope — both extend beyond the strict boundary the analysis set.

**Resolution: DISMISSED** — Decision log entry #6 records the HCPCS approval flag inclusion as a deliberate choice (costs nothing to store now; skipping requires a data migration later). MSRP is required for self-pay orders per §4.3/FR-7. Both extensions are documented and defensible.

---

**5. Six-problem inventory not mapped to PRD sections**
> The PRD's vision summarized problems at a high level but did not trace which FRs address which problems.

**Resolution: DISMISSED** — Addressed by the problem taxonomy update applied 2026-05-27: §1 executive summary now names all four problems; §5 Non-Goals restructures deferrals by problem type; §6.2 Out of Scope table now includes a Problem column mapping each deferred capability to its problem type.

---

## Resolution Summary

| Gap | Source | Resolution |
|---|---|---|
| Scope discipline constraint | problem-statement | Dismissed — PM concern, covered implicitly by §5 |
| Auditability requirement | problem-statement | Dismissed — covered by NFR-2 |
| Submitted order immutability | problem-statement | → OQ-6 in §8 |
| Baseline capture as gate | problem-statement | Applied — §7 elevated to named pre-launch gate |
| Lead time timestamp | problem-statement | → OQ-7 in §8 |
| Compliance risk dimensions | problem-space-analysis | Dismissed — subsumed by OQ-6 and NFR-2 |
| Access controls | problem-space-analysis | Dismissed — covered by NFR-1 |
| Data model alongside form | problem-space-analysis | Applied — §9 Assumptions Index |
| HCPCS/MSRP scope expansion | problem-space-analysis | Dismissed — decision log entry #6 |
| Six-problem mapping | problem-space-analysis | Dismissed — addressed by 2026-05-27 PRD update |

**All 10 gaps resolved. No open items remaining.**
