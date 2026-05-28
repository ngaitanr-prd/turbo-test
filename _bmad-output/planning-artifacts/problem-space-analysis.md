# Problem Space Analysis
**Project:** turbo-test
**Date:** 2026-05-27
**Participants:** Nicolas (PM), John (AI Product Manager)
**Source material:** Initial conversation transcript (Alex & Camila)

---

## Context

Alex is a medical supply distributor serving physical therapy clinics treating lymphedema and breast cancer patients. The business receives orders from therapists, handles insurance verification, prior authorizations, vendor ordering, and billing — all currently managed inside a large Excel spreadsheet. Alex wants to replace this with a web-based internal tool.

---

## Problem Inventory

Six distinct problems were identified from the initial conversation:

| ID | Problem | Description |
|----|---------|-------------|
| P1 | Fragile, Opaque Workflow Tooling | The operational workflow runs on a spreadsheet where logic is hidden, interdependent, and fails silently. A single broken field can corrupt the entire process. |
| P2 | Business Logic Has No Canonical Home | Pricing rules, fee schedules, payer rates, vendor behavior, and prior auth requirements live scattered across hidden spreadsheet tables and people's heads. |
| P3 | Manual Re-Entry Across Disconnected Systems | Data entered once gets typed again — into vendor portals, patient record systems, DocuSign. The team serves as human middleware. |
| P4 | Compliance Controls Are Detached from the Workflow | The manager approval gate for certain HCPCS codes lives in SharePoint, outside the order flow. It can be bypassed or forgotten. |
| P5 | Document Generation Is a Manual Ritual | Producing the three required documents requires a multi-step export process instead of being a natural output of completing an order. |
| P6 | Tribal Knowledge Owns Critical Decisions | Prior auth requirements, vendor routing logic, and self-pay overrides exist only in experienced staff members' heads. |

---

## Consolidated Problem Categories

Revised table incorporating: removal of "Scalability Constraints" as a standalone category (absorbed into Growth Impact), merger of "Pricing & Revenue Integrity" into "Canonical Source of Knowledge & Data Management", and addition of Compliance Risk as a fourth impact dimension.

| Problem Category | Specific Problem | Signals From Alex | Operational Cost Impact | Revenue Impact | Compliance Risk Impact | Growth Impact | ROI |
|---|---|---|---|---|---|---|---|
| **Manual Work & Administrative Overhead** | Manual re-entry into vendor portals | "our team has to re-enter everything manually in the vendor portals" | High admin labor; employee time wasted on repetitive tasks | Slower fulfillment and billing cycles; increased order errors | Low | Scaling requires proportional headcount growth — direct cap on throughput | Very High |
| **Manual Work & Administrative Overhead** | Manual document generation and handling | "we save the documents as PDFs, upload them…" | Time spent generating, saving, uploading, organizing documents | Incorrect or missing docs may delay payment or reimbursement | Medium — missing documents can constitute a compliance gap in patient records | Document burden grows linearly with order volume | High |
| **Manual Work & Administrative Overhead** | Lack of automated vendor routing/emailing | "If the system could detect the vendor and send the order automatically" | Manual routing and communication effort per order | Order processing delays slow fulfillment and cash flow | Low | Without automation, operational throughput cannot grow without equivalent staffing | High |
| **Human-Dependent Workflows** | Manual approvals for HCPCS codes | "certain HCPCS codes require a manager's approval" and "manual approval flow" | Manager dependency; approval bottlenecks; admin overhead | Delayed order progression and delayed reimbursement | High — no audit trail proving approval occurred before fulfillment; regulatory exposure if audited | Hard to enforce approval rules consistently as team and volume grow | High |
| **Human Errors & Operational Risk** | Fragile spreadsheet logic | "If one field breaks, the whole sheet goes haywire" | Troubleshooting overhead; dependency on spreadsheet expertise; operational disruptions | Incorrect pricing, billing, or reimbursement calculations; margin leakage | Medium — billing errors in insurance claims can trigger audits or recoupment demands | Maintenance burden grows exponentially as rules, products, and payers increase | Very High |
| **Human Errors & Operational Risk** | Complex pricing and reimbursement logic embedded in spreadsheets | "logic depends on the vendor, product type, state, or payer" and "pulls from hidden tables" | Ongoing spreadsheet maintenance; difficult validation and updates | Billing inaccuracies, claim issues, incorrect patient balances, margin risk | Medium — opaque logic makes it hard to demonstrate billing compliance if audited | Adding new vendors/payers/products increases operational fragility | Very High |
| **Human Errors & Operational Risk** | High cognitive load on employees | Employees must hold pricing logic, approvals, documents, vendor processes in their heads | Increased training burden; higher probability of human error | Errors may affect orders, billing, reimbursement, or patient experience | Low | Team efficiency declines as operational complexity increases; onboarding slows | High |
| **Canonical Source of Knowledge & Data Management** | Lack of centralized structured data | Alex wants "two tables: one for products… and one for fee schedules" | Inconsistent data management; manual lookups; difficult maintenance | Pricing and reimbursement inconsistencies | Low | Difficult to standardize or automate workflows without a data foundation | High |
| **Canonical Source of Knowledge & Data Management** | Heavy reliance on tribal knowledge | "We know that internally, but it's not written anywhere yet" | Long onboarding/training time; reliance on experienced employees | Missed prior authorizations or inconsistent execution affect reimbursement | Medium — undocumented rules mean compliance cannot be audited or demonstrated | Difficult to scale teams consistently; institutional knowledge is a single point of failure | High |
| **Canonical Source of Knowledge & Data Management** | Lack of embedded prior authorization tracking | "I'd love to eventually track whether certain items require prior authorization" | Manual checking and dependency on employee memory | Missing authorizations lead to claim denials or payment delays | High — prior auth is a payer requirement; skipping it can result in claim denial, recoupment, or exclusion | Rules become harder to manage as payer/product complexity grows | Very High |
| **Canonical Source of Knowledge & Data Management** | Self-pay pricing has no canonical rule | "price should default to the MSRP from the vendor catalog" | Manual pricing verification per order | Incorrect patient invoices or inconsistent pricing | Low | Additional pricing scenarios increase operational complexity without a single source of truth | Medium |
| **Workflow Fragmentation & System Complexity** | Excel acting as the operational backbone | "we manage all of our patient orders and billing flows inside a huge Excel spreadsheet" | Operational inefficiency from using a non-scalable tool for core workflows | Revenue operations depend on unstable, manual processes | Medium — no audit trail, data integrity risk, no access controls on sensitive patient/billing data | Tooling becomes a direct bottleneck to operational maturity — this is the root of the scalability ceiling Alex describes | Very High |
| **Workflow Fragmentation & System Complexity** | Fragmented workflow across systems | Workflow spans Excel, SharePoint, PDFs, DocuSign, email, vendor portals, internal systems | Context switching; manual coordination; duplicate uploads and communications | Delays in order completion, invoicing, and reimbursement | Low | Operational complexity compounds with volume; coordination cost grows non-linearly | High |
| **Workflow Fragmentation & System Complexity** | Measurement forms managed outside a structured workflow | "We should be able to upload those per line item" | Administrative coordination and file management overhead | Missing required documentation may delay fulfillment or reimbursement | Low | Supporting more complex product requirements becomes harder at scale | Medium |

---

## Prioritization Reasoning

### Why "Canonical Source of Knowledge & Data Management" first

This category is not just high ROI — it is a **prerequisite** for ROI in every other category:

- You cannot reliably automate vendor routing if vendor rules aren't written down
- You cannot enforce HCPCS approval gates if you don't know which codes require them
- You cannot auto-populate a form with pricing if the pricing logic is opaque and context-dependent
- You cannot track prior auth if no one has codified which products need it

Automating on top of bad or scattered data doesn't solve the problem — it propagates errors faster.

### Adversarial challenges considered

| Challenge | Response |
|---|---|
| "Data foundation first" is a classic over-engineering trap | Mitigated by delivering a visible form alongside the data layer — not infrastructure alone |
| The "automating a mistake" risk may be overstated | Alex's data may be mostly correct but poorly structured — still, canonical structure is the prerequisite for reliable automation |
| You don't know what the data layer needs until you build what consumes it | Mitigated by designing the data model alongside the first form, not before it |
| "Canonical Source" bundles four different problems | Mitigated by scoping only to centralized structured data (products + fee schedules) in the first pass |
| Compliance risk might force a different starting point | HCPCS approval tracking is acknowledged as high compliance risk; deferred as a second effort |

---

## Decision

**Problem to attack first:**
> Alex's team has no reliable, centralized source of product and pricing data. That data lives in hidden Excel tables and people's heads — making it opaque, fragile, and unsafe to automate against.

**Scope of first effort:**
- Build a centralized product table and fee schedule table
- Scope the data model to exactly what the first order entry form needs — nothing more
- Deliver through the first form that consumes it, so value is immediately visible

**Boundary to hold:**
The temptation will be to also capture tribal knowledge, add prior auth rules, and handle self-pay while "already in there." Scope discipline is critical — the first form ships with product data and fee schedules only.

---

## Qualitative ROI Rationale

The problem we are attacking first — **Lack of centralized structured data** — has a **High** qualitative ROI on its own. The stronger argument is what it unlocks:

| Problem | Qualitative ROI | Status |
|---|---|---|
| Lack of centralized structured data | High | **Attacking now** |
| Fragile spreadsheet logic | Very High | Unblocked by this |
| Complex pricing logic embedded in spreadsheets | Very High | Unblocked by this |
| Excel acting as the operational backbone | Very High | Unblocked by this |
| Manual re-entry into vendor portals | Very High | Unblocked by this |
| Lack of prior authorization tracking | Very High | Unblocked by this — deferred |

We are solving a **High** ROI problem that is the direct prerequisite to five **Very High** ROI problems. Without it, none of those five are safe to build — automating on top of scattered, untrustworthy data would propagate existing errors faster.

---

## Deferred Problems

The following problems were identified and scoped, but explicitly left for a later moment. They are sequenced after the canonical data foundation is in place.

| Problem | Category | Qualitative ROI | Why Deferred |
|---|---|---|---|
| Manual re-entry into vendor portals | Manual Work & Administrative Overhead | Very High | Requires reliable data foundation to automate safely |
| Lack of automated vendor routing/emailing | Manual Work & Administrative Overhead | High | Requires vendor rules to be canonical first |
| Manual document generation and handling | Manual Work & Administrative Overhead | High | Requires stable order data to generate correctly |
| Manual approvals for HCPCS codes | Human-Dependent Workflows | High | Compliance-critical but distinct effort; requires knowing which codes need approval — a rules/data problem |
| Fragile spreadsheet logic | Human Errors & Operational Risk | Very High | Resolved as a consequence of moving off Excel |
| Complex pricing logic embedded in spreadsheets | Human Errors & Operational Risk | Very High | Resolved by migrating logic into the canonical data layer |
| High cognitive load on employees | Human Errors & Operational Risk | High | Reduced as system encodes rules currently held in people's heads |
| Heavy reliance on tribal knowledge | Canonical Source of Knowledge & Data Management | High | Process/documentation problem — distinct from data structure problem |
| Lack of embedded prior authorization tracking | Canonical Source of Knowledge & Data Management | Very High | High compliance value; deferred to keep first effort scoped |
| Self-pay pricing has no canonical rule | Canonical Source of Knowledge & Data Management | Medium | Configuration problem; can be added as a rule in the data layer later |
| Fragmented workflow across systems | Workflow Fragmentation & System Complexity | High | Addressed progressively as individual tools are replaced |
| Measurement forms managed outside a structured workflow | Workflow Fragmentation & System Complexity | Medium | Low urgency; can be added as a file attachment feature later |

---

## Success Outcomes

Outcomes that can be observed without introducing new measurement overhead:

| Outcome | How to Measure |
|---|---|
| Order throughput increases | Count orders processed per week/month — same team, more output |
| Order lead time decreases | Track time from clinic order received to order placed with vendor |
| Correction and rework rate decreases | Count orders that required a pricing or data correction after entry per month |
| Staff independence increases | Observable without measurement — less experienced staff complete orders without asking for help |
| Claim denial rate decreases | Already reported by insurance — fewer denials attributable to billing data errors |

**Baseline note:** Alex's team should capture current figures for throughput, lead time, and correction rate before the build begins. Without a before number, the after cannot be demonstrated.

---

## Next Steps

- [ ] Write formal problem statement
- [ ] Move into PRD (`/bmad-prd`)
