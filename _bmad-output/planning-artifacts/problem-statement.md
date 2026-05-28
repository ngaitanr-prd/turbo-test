# Problem Statement
**Project:** turbo-test
**Date:** 2026-05-27
**Informed by:** problem-space-analysis.md

---

## Problem We Are Solving Now

Alex's team currently has no reliable, centralized source of product and pricing data. Business rules — including product costs, vendor fee schedules, payer rates, and billing logic — are distributed across hidden Excel tables, undocumented spreadsheet formulas, and the memory of experienced staff.

As a result, every order entry depends on an individual employee's understanding of those rules. The same order processed by two different people can produce different prices, different margins, and different patient balances. Errors are hard to catch before they reach billing. And any automation built on top of this foundation inherits every mistake and gap already in it — making future improvements not just difficult, but unsafe.

**The problem we are solving:** Alex's team cannot trust that the data underlying their order entry process is correct, consistent, or auditable — which makes the entire downstream workflow unreliable.

**What success looks like:**
- A single, trustworthy source for product data and fee schedules that the team relies on instead of the spreadsheet
- An order entry form that consumes that data, so the same inputs always produce the same output regardless of who processes the order
- A foundation that makes every subsequent automation safe to build

**Outcomes we will observe:**
- Order throughput increases — same team, more orders processed per week/month
- Order lead time decreases — less time from clinic order received to order placed with vendor
- Correction and rework rate decreases — fewer orders requiring a pricing or data fix after entry
- Staff independence increases — less experienced employees complete orders without needing guidance
- Claim denial rate decreases — fewer denials attributable to billing data errors

---

## Problems We Know Exist — Deferred to a Later Stage

The following problems were identified, scoped, and intentionally deferred. They are sequenced after the canonical data foundation is proven and stable. Solving them prematurely — before the data layer is trustworthy — risks automating errors rather than eliminating them.

---

### Stage 2 — Automate on Top of the Foundation

These problems become safe to attack once the canonical data layer exists.

**Manual re-entry into vendor portals** *(Very High ROI)*
Alex's team re-enters order data manually into vendor portals after it has already been captured in the system. This is a direct target for automation once the data source is reliable — the system can route and submit orders to the correct vendor without human re-entry.

**Lack of automated vendor routing and emailing** *(High ROI)*
The logic for which vendor receives which order exists only in staff knowledge. Once vendor rules are canonical, the system can detect the vendor and send the order automatically.

**Manual document generation and handling** *(High ROI)*
Encounter forms, patient invoices, and proofs of delivery are generated manually, saved as PDFs, and uploaded by hand. Once order data is structured and reliable, these documents can be generated as a natural output of completing an order.

---

### Stage 3 — Compliance and Rules Engine

These problems require a rules engine on top of the data foundation and carry the highest compliance exposure.

**Manual approvals for HCPCS codes** *(High ROI)*
Certain HCPCS codes require manager approval before an order proceeds. This gate currently lives outside the workflow in SharePoint, with no audit trail. Once the system knows which codes require approval, this control can be enforced and logged within the order flow.

**Lack of embedded prior authorization tracking** *(Very High ROI)*
Which products require prior authorization from a payer is tribal knowledge. Missing a required prior auth leads to claim denials and potential recoupment. Once the canonical data layer exists, prior auth rules can be attached to products and enforced at order entry.

---

### Stage 4 — Operational Completeness

These problems are real but lower urgency. They round out the system once the core is stable.

**Heavy reliance on tribal knowledge** *(High ROI)*
Pricing rules, vendor behaviors, and process exceptions exist only in experienced employees' heads. This creates onboarding risk and key-person dependency. Addressed progressively as the system encodes rules that were previously undocumented.

**High cognitive load on employees** *(High ROI)*
Staff must currently hold pricing logic, approval requirements, document flows, and vendor processes in their heads simultaneously. This decreases as the system takes on that responsibility.

**Self-pay pricing has no canonical rule** *(Medium ROI)*
Self-pay orders should default to MSRP from the vendor catalog, but this is currently a manual override. Can be added as a configuration rule in the data layer once the foundation is stable.

**Measurement forms managed outside a structured workflow** *(Medium ROI)*
Therapist measurement forms are handled outside the order flow. Can be addressed as a file attachment feature attached to line items once the core order structure exists.

**Fragmented workflow across systems** *(High ROI)*
The workflow spans Excel, SharePoint, PDFs, DocuSign, email, and vendor portals. Addressed progressively as each stage replaces a manual step with a system-driven one.
