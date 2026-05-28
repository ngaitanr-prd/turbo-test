# PRD Reconciliation: Gaps Against Source Documents
**PRD:** prd.md (Canonical Data Layer and Order Entry Form)
**Sources:** problem-statement.md, problem-space-analysis.md
**Date:** 2026-05-27

---

## Source 1: problem-statement.md

### Gaps and Missing Items

**1. Scope boundary / discipline constraint not reflected**
The problem statement explicitly warns: *"The temptation will be to also capture tribal knowledge, add prior auth rules, and handle self-pay while 'already in there.' Scope discipline is critical."* The PRD's §5 non-goals list covers the outcomes of this discipline but does not articulate the discipline itself as a design principle or risk to manage. No PM note flags scope creep as an active risk.

**2. Auditability as an explicit requirement**
The problem statement frames the core failure as data that is not "auditable." The PRD does not include any requirement for audit trails — who entered an order, when, or what data was used at the time of submission. This is absent from both the FRs and the open questions.

**3. "Same inputs, same output" stated as a goal but not formalized as a requirement**
The problem statement's success definition includes: *"An order entry form...so the same inputs always produce the same output regardless of who processes the order."* FR-4 addresses deterministic rate lookup, but no FR explicitly requires deterministic end-to-end order output (e.g., locking computed values at submission so historical records cannot silently change if catalog data changes later).

**4. Baseline capture stated as a prerequisite — not surfaced as an action item**
The problem statement includes: *"Alex's team should capture current figures before the build begins."* The PRD's §7 baseline note repeats this but does not designate it as an action item, a dependency, or a pre-launch gate. It risks being overlooked before deployment.

**5. Order lead time metric scoping**
The problem statement defines lead time as "time from clinic order received to order placed with vendor." The PRD's SM-2 repeats this definition, but the system does not yet capture a "clinic order received" timestamp — this data point cannot be measured without a field to record it. No FR or open question addresses this gap.

---

## Source 2: problem-space-analysis.md

### Gaps and Missing Items

**1. Compliance risk dimensions not reflected in requirements**
The problem space analysis rates several problems by compliance risk impact. Billing errors in insurance claims can "trigger audits or recoupment demands." The PRD does not include any requirement related to data integrity assurance (e.g., immutability of submitted records, field-level validation tied to billing compliance). Compliance exposure is acknowledged in non-goals but not translated into v1 guardrails.

**2. Access controls on sensitive patient/billing data**
The analysis explicitly flags: *"no access controls on sensitive patient/billing data"* as a compliance-medium risk of the current Excel setup. The PRD has no requirement — not even a deferred note — about authentication, role-based access, or data access controls. This is a meaningful gap for a system handling patient and insurance data.

**3. The adversarial challenge "you don't know what the data model needs until you build what consumes it" is not reflected in the PRD**
The analysis documents a specific mitigation: *"design the data model alongside the first form, not before it."* The PRD does not reflect this as a delivery constraint or development approach note. If the data model is designed before the form, the risk the analysis flagged is not mitigated.

**4. "Scope the data model to exactly what the first order entry form needs — nothing more" — not enforced**
The analysis specifies a hard boundary: the first form ships with product data and fee schedules only, and the scope boundary must be held. The PRD includes the HCPCS approval-required flag (captured for future use) and the MSRP field — both explicitly listed as in-scope in §6.1. These are defensible extensions, but the PRD does not acknowledge that they represent a deliberate scope expansion relative to the analysis's stated boundary, or that the boundary was consciously relaxed.

**5. Six-problem inventory not mapped to PRD sections**
The problem space analysis identifies six distinct problems (P1–P6). The PRD's §1 vision summarizes them at a high level but does not trace which FRs address which problems. P1 (fragile workflow tooling), P3 (manual re-entry), P4 (compliance controls detached from workflow), P5 (document generation), and P6 (tribal knowledge) are either deferred or out of scope — but the PRD does not make this mapping explicit. A reader cannot confirm that no in-scope problem was accidentally dropped.

---

## Contradictions

**None identified.** The PRD is consistent with both source documents. The deferred items in the PRD align with the sequencing defined in both the problem statement and the problem space analysis.

---

## Summary

| Category | Count |
|---|---|
| Gaps from problem-statement.md | 5 |
| Gaps from problem-space-analysis.md | 5 |
| Contradictions | 0 |

**Highest priority gaps to resolve before PRD is finalized:**
1. Audit trail / data immutability requirements (missing from FRs entirely)
2. Access controls on patient and billing data (missing from FRs and open questions)
3. "Clinic order received" timestamp — required to measure SM-2 but no FR captures it
4. Baseline capture formalized as a pre-launch dependency, not just an advisory note
