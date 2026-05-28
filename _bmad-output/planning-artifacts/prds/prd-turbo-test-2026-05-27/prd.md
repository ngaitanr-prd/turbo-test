---
title: Canonical Data Layer and Order Entry Form
status: draft
created: 2026-05-27
updated: 2026-05-27
---

# PRD: Canonical Data Layer and Order Entry Form

## 0. Document Purpose

This PRD is for the PM, stakeholders, and downstream workflow owners involved in the first product effort for turbo-test. It is structured with a Glossary-anchored vocabulary, features grouped with globally numbered FRs nested under them, and assumptions tagged inline and indexed in §9. It is informed by the problem space analysis, problem statement, and refined problem statement in `_bmad-output/planning-artifacts/`. It describes capabilities only — mechanism and technology decisions are deferred to the solution design phase.

---

## 1. Vision

**Executive summary**

Alex's business has outgrown the spreadsheet holding it together. Four distinct problems were identified: unreliable master data (Problem 1), people serving as middleware between disconnected systems (Problem 2), compliance controls detached from the workflow (Problem 3), and critical process knowledge existing only in people's heads (Problem 4). This product attacks Problem 1 — establishing a single, reliable source of product and pricing data so that order entry is consistent, corrections drop, and every automation that follows is built on something the team can trust. Problems 2–4 are explicitly deferred and sequenced in later stages.

---

Alex's business runs on a workflow that was never designed to scale. Patient orders, insurance billing, pricing logic, and vendor rules are all managed through a spreadsheet that has grown too complex to trust and too fragile to automate against. This product is the first move toward changing that.

The immediate goal is narrow and deliberate: establish a single, reliable source of product and pricing data, and deliver it through the first order entry form that consumes it. For Alex's team, this means one workflow becomes noticeably more organized — less reprocessing, fewer corrections, and less dependence on any individual's knowledge of the rules.

The strategic weight is larger than the scope. Every improvement Alex wants downstream — automated vendor routing, document generation, compliance controls — is only safe to build once the data underneath it is trustworthy. This first step is what makes the rest of the roadmap buildable. Done right, it begins moving the business from a fragile, people-dependent operation toward one where the system carries the rules and the team focuses on the work.

The Order Entry Form is not a separate problem from the data layer — it is the enforcement mechanism that closes the behavioral loop. The canonical catalog and fee schedule make the data reliable; the Form makes employees consume that reliable data instead of the legacy spreadsheet. Without the Form, the data fix is structural but not operational. All three components — Product Catalog, Fee Schedule, Order Entry Form — are necessary to fully resolve Problem 1.

---

## 2. Target User

### 2.1 Jobs To Be Done

- Enter a patient order correctly without needing to know pricing rules, fee schedules, or vendor logic by heart
- Trust that the system produces consistent output regardless of who is processing the order
- Complete order entry without switching between tools, looking up hidden tables, or asking a more experienced colleague

### 2.2 Non-Users (v1)

- **Managers** — approval flows are deferred to a later stage
- **Clinicians and therapists** — they submit orders externally; this tool is for internal processing only
- **Patients** — this is not a patient-facing product
- **Vendors** — vendor communication is deferred to a later stage

---

## 3. Glossary

- **Order** — A request received from a clinic on behalf of a patient for one or more medical supply products. The primary unit of work in the system.
- **Line Item** — A single product within an Order, with its own quantity, pricing, and billing details.
- **Product** — A medical supply item carried in the catalog, identified by vendor, category, and HCPCS code.
- **HCPCS Code** — A standardized billing code that identifies a product category for insurance reimbursement purposes.
- **Vendor** — The supplier from whom products are sourced and drop-shipped to the patient.
- **Payer** — The insurance company responsible for reimbursing the order.
- **Fee Schedule** — A table of reimbursement rates per HCPCS code, defined per Payer. Determines billable amounts.
- **Product Catalog** — The centralized table of all Products, including cost, vendor, category, and HCPCS code.
- **Billable Amount** — The amount submitted to the Payer for reimbursement, derived from the Fee Schedule.
- **Patient Responsibility** — The portion of the Billable Amount owed by the patient after insurance.
- **Margin** — The difference between the Billable Amount and the Product cost.
- **MSRP** — Manufacturer's Suggested Retail Price. Used as the default price for self-pay Orders.
- **Self-Pay** — An Order where the patient is not covered by insurance and pays out of pocket at MSRP.
- **Drop Ship** — The fulfillment model where the Vendor ships directly to the patient.

---

## 4. Features

### 4.1 Product Catalog

**Description:** The system maintains a single, authoritative source of product data that employees reference during order entry. The catalog stores all Products available for ordering, with the fields required to identify, price, and bill each item correctly. The catalog is maintainable — Products can be added or updated — though the mechanism for doing so is deferred to the solution design phase. Each HCPCS code carries a flag indicating whether it requires manager approval; this flag is captured now so downstream approval workflows can consume it without a data migration.

**Functional Requirements:**

#### FR-1: Product record
The catalog must store the following per Product: name, Vendor, product category, HCPCS code, unit of measure (UoM), unit cost, and MSRP. Each HCPCS code must carry a flag indicating whether it requires manager approval before an Order proceeds.

**Consequences:**
- Any Product selected during order entry has a complete, retrievable record with all fields populated
- MSRP is always present and accessible for self-pay Orders
- Every HCPCS code has an explicit approval-required flag, readable by downstream workflows when the approval gate is built

#### FR-2: Product availability for order entry
Employees can select any active Product from the catalog when filling out an Order.

**Consequences:**
- Only active Products are selectable during order entry
- A Product not in the catalog cannot be added to an Order

---

### 4.2 Fee Schedule Management

**Description:** The system maintains a single, authoritative source of Payer reimbursement rates. Because rates vary by Payer, HCPCS code, and patient ZIP code — and the same Payer may have different rates depending on whether the patient's location is rural, non-rural, or within a former Competitive Bidding Area — the Fee Schedule must support multi-dimensional lookups keyed by ZIP code. Rates may include a multiplier applied to a base rate; the exact behavior of the multiplier requires clarification from Alex (see OQ-3).

**Functional Requirements:**

#### FR-3: Fee schedule record
The Fee Schedule must store the following per entry: Payer, HCPCS code, patient ZIP code, base rate, and multiplier.

**Consequences:**
- A unique rate can be defined for any combination of Payer, HCPCS code, and patient ZIP code
- The multiplier field exists on every record, even if not always applied

#### FR-4: Rate lookup
Given the Payer, HCPCS code, and patient ZIP code on an Order, the system retrieves the correct Fee Schedule entry.

**Consequences:**
- The lookup is deterministic — the same inputs always return the same rate
- If no matching entry exists, the system surfaces an explicit error rather than silently applying a wrong or default rate

---

### 4.3 Order Entry Form

**Description:** Employees enter a patient Order by providing patient information, selecting a payment type, and adding one or more Products from the catalog. Pricing, billing, and Margin fields auto-populate based on the payment type and the data in the Product Catalog and Fee Schedule — employees do not look up or enter these values manually. Payment type is set at the Order level and applies to all Line Items. A review and confirmation step before submission is explicitly deferred to a later stage.

**Functional Requirements:**

#### FR-5: Patient information capture
The form captures the following at the Order level: patient name, insurance information, shipping address, and payment type (Self-Pay or insurance).

**Consequences:**
- All four fields are required before an Order can be submitted
- Payment type applies to all Line Items on the Order

#### FR-6: Product line item entry
Employees can add one or more Products to an Order by selecting from the active Product Catalog. Each Line Item captures product and quantity; UoM and HCPCS code are derived from the catalog selection.

**Consequences:**
- Only active catalog Products are selectable
- An Order must have at least one Line Item to be submitted

#### FR-7: Pricing auto-population
When a Product is selected and payment type is set, the system automatically derives pricing without employee input:
- **Self-Pay:** unit price defaults to MSRP from the catalog
- **Insurance:** unit price is retrieved from the Fee Schedule using Payer, HCPCS code, and state from the patient's shipping address

**Consequences:**
- Employees cannot manually override an auto-populated price `[ASSUMPTION: price overrides are not permitted in v1]`
- If no matching Fee Schedule entry exists, the system surfaces an explicit error on that Line Item

#### FR-8: Billing calculation
The system calculates and displays per Line Item: Billable Amount (base rate × multiplier × quantity), unit cost, and Margin.

**Consequences:**
- Calculated fields update automatically when Product or quantity changes
- Margin is always visible to the employee at Line Item level

#### FR-9: Order received timestamp
The system records the date and time an Order is created.

**Consequences:**
- Every Order has a creation timestamp that is set by the system, not entered manually
- The timestamp is preserved and readable for reporting — enabling SM-2 (order lead time) to be measured

---

## 4.4 Cross-Cutting Non-Functional Requirements

These requirements apply to the system as a whole, not to a single feature.

#### NFR-1: Access controls
The system must restrict access to patient and billing data to authorized internal staff only. `[ASSUMPTION: all users in v1 are internal employees with equivalent access — role-based access control is deferred to a later stage]`

**Consequences:**
- Unauthorized users cannot view, enter, or modify Orders, the Product Catalog, or Fee Schedules
- The access model is defined at deployment; the mechanism is a solution design decision

**Out of Scope (later):** Role-based access control, manager vs. employee permission tiers, audit-based access restrictions.

#### NFR-2: Basic auditability
The system must record who submitted each Order and when.

**Consequences:**
- Every submitted Order is associated with the employee who created it and the creation timestamp (FR-9)
- This record is preserved and cannot be modified after submission

**Out of Scope (later):** Field-level change history, edit logs, full audit trails for catalog and fee schedule changes.

---

## 5. Non-Goals

What this product will not do in this delivery. Each deferral is a deliberate sequencing decision — not a scope cut — tied to one of the four identified problems:

**Problem 2 — Integration (Stage 2):** These capabilities require a stable data foundation before automation is safe to build on top of it.
- Generate documents — encounter forms, patient invoices, and proofs of delivery are not produced by this system in v1
- Automate vendor communication — Orders are not routed or emailed to Vendors automatically

**Problem 3 — Governance (Stage 3):** Compliance controls can only be reliably enforced once the underlying data layer is trustworthy. Enforcing rules against unreliable data would produce false confidence, not compliance.
- Enforce approval gates — HCPCS codes flagged as requiring manager approval are captured in the catalog but the approval workflow is not enforced
- Track prior authorization — prior auth rules are not enforced or surfaced during order entry

**Problem 4 — Knowledge (Stage 4):** These require the core system to be stable before undocumented process knowledge can be progressively encoded into it.
- Document and encode tribal knowledge — vendor routing logic, pricing edge cases, and process exceptions exist only in people's heads; encoding them is deferred until the system can carry them reliably
- Support measurement form uploads per Line Item

**Out of scope regardless of stage:**
- Replace DocuSign or payment flows — patient signatures and payment collection are out of scope
- Manage Self-Pay pricing rules beyond MSRP defaulting

---

## 6. MVP Scope

### 6.1 In Scope

- Centralized Product Catalog with all fields required for order entry and billing
- Fee Schedule table supporting multi-dimensional rate lookup by Payer, HCPCS code, and state
- Order entry form that auto-populates pricing and billing from the catalog and Fee Schedule
- Self-Pay and insurance payment types at Order level
- HCPCS approval-required flag stored in catalog, readable by future workflows

### 6.2 Out of Scope for MVP

| Capability                                         | Problem          | Deferred To                                                 |
| -------------------------------------------------- | ---------------- | ----------------------------------------------------------- |
| Automated vendor routing and order emailing        | P2 — Integration | Stage 2                                                     |
| Document generation (encounter form, invoice, POD) | P2 — Integration | Stage 2                                                     |
| Manager approval gate enforcement for HCPCS codes  | P3 — Governance  | Stage 3                                                     |
| Prior authorization tracking and enforcement       | P3 — Governance  | Stage 3                                                     |
| Tribal knowledge encoding (routing, pricing rules) | P4 — Knowledge   | Stage 4                                                     |
| Measurement form uploads per Line Item             | P4 — Knowledge   | Stage 4                                                     |
| Self-Pay pricing configuration beyond MSRP         | P4 — Knowledge   | Stage 4                                                     |
| Fragmented workflow consolidation across systems   | P2 + P3 + P4     | Progressive — resolved as each stage replaces a manual step |

---

## 7. Success Metrics

*Each SM cross-references the FR(s) it validates.*

**Primary**
- **SM-1:** Order throughput — orders processed per week/month by the same team. Target: measurable increase after deployment. Validates FR-6, FR-7, FR-8.
- **SM-2:** Order lead time — time from clinic order received to order placed with vendor. Target: reduction from current baseline. Validates FR-5, FR-6, FR-7.
- **SM-3:** Correction and rework rate — number of orders requiring a pricing or data correction after submission per month. Target: reduction from current baseline. Validates FR-7, FR-8.

**Secondary**
- **SM-4:** Staff independence — less experienced employees complete orders without requesting guidance. Observable without formal measurement. Validates FR-7.
- **SM-5:** Claim denial rate — denials attributable to billing data errors, as reported by Payers. Target: reduction from current baseline. Validates FR-8.

**Counter-metrics (do not optimize)**
- **SM-C1:** Order submission speed should not be optimized at the expense of data completeness — a fast form with missing or wrong fields is worse than a slower correct one. Counterbalances SM-1 and SM-2.

**Baseline note:** Alex's team should capture current figures for SM-1, SM-2, and SM-3 before deployment. Without a before number the after cannot be demonstrated.

---

## 8. Open Questions

1. **OQ-1** *(closed)* — HCPCS approval flag: captured at the product catalog level. Enforcement deferred to Stage 3.
2. **OQ-2** — Measurement forms: are they required at the product level or HCPCS level? Needed before the upload mechanism is designed in Stage 4.
3. **OQ-3** — Multiplier behavior: does the Billable Amount always equal base rate × multiplier, or does this vary by Payer or product type? Needs clarification from Alex.
4. **OQ-4** — Patient responsibility calculation: research indicates this requires inputs unlikely to be available at order entry (deductible met, coinsurance %, OOP max). Likely cannot be auto-calculated in v1. Needs clarification from Alex on whether it should be a manually entered field or deferred entirely.
5. **OQ-5** *(closed)* — Geographic lookup key for DMEPOS fee schedules is the patient's ZIP code, not the state. Rural/non-rural classification and former Competitive Bidding Areas both use ZIP code. FR-3 and FR-4 updated accordingly.

---

## 9. Assumptions Index

- **§4.3 / FR-7** — Price overrides are not permitted in v1. Employees cannot manually change an auto-populated price.
- **§4.4 / NFR-1** — All v1 users are internal employees with equivalent access. Role-based access control is deferred to a later stage.
