---
stepsCompleted: [1, 2, 3]
inputDocuments: ['_bmad-output/planning-artifacts/prds/prd-turbo-test-2026-05-27/prd.md']
session_topic: 'Solution approaches for canonical product/pricing data layer and order entry form'
session_goals: 'Explore different ways to solve the problem — not just technology options, but fundamentally different approaches to establishing reliable data and an order entry experience'
selected_approach: 'Option 1 (Web App) + Mining + Rule-based fee schedule'
techniques_used: ['Alien Anthropologist', 'First Principles Thinking', 'Pirate Code Brainstorm']
context_file: '_bmad-output/planning-artifacts/prds/prd-turbo-test-2026-05-27/prd.md'
---

# Brainstorming Session Results

**Facilitator:** Nicolas
**Date:** 2026-05-27

## Session Overview

**Topic:** Solution approaches for Alex's canonical data layer and order entry form
**Goals:** Explore different ways — architecturally, experientially, and operationally — to establish a reliable Product Catalog, Fee Schedule, and Order Entry Form

### Context
- Medical supply distributor, internal tool for a small team
- Problem: no single reliable source for product/pricing data — lives in Excel and people's heads
- Scope: Product Catalog + Fee Schedule (Payer × HCPCS × ZIP code) + Order Entry Form with auto-populated pricing/billing
- PRD complete; brainstorming solutions before architecture/tech decisions

---

## Solution Dimensions Explored

### Order Entry Options

**Option 1 — Web App**
Employee opens a structured web form, enters patient info, selects products from a catalog dropdown. System auto-populates HCPCS, pricing, and billing fields. Employee reviews and submits.

**Option 2 — AI-assisted entry (platform-agnostic)**
AI reads an incoming clinic document (fax, email, PDF), extracts patient info and product selections, and pre-fills the form. Employee reviews and corrects. System auto-populates pricing and billing. Platform-agnostic — can be delivered through any interface.

**Option 3 — Clinic-side intake**
Clinic fills a structured intake form directly in a portal Alex provides. Structured data arrives in Alex's system with pricing already calculated. Employee reviews and approves.

**Option X — Excel as order entry interface (explored and rejected)**
Keep Excel as the order entry surface but connect it to a canonical database and rules engine via external data connections. Employee experience unchanged — Excel calls the rules engine for pricing.

*Rejected because:* Excel is the problem, not just the tool. Keeping it as the interface preserves silent failures, no access controls on patient/billing data, no audit trail, no data integrity constraints, and no surface for Stage 2–4 features (document generation, vendor routing, approval gates) to live on. Mining and rules engine ideas are sound — keeping Excel as the front-end wastes them.

---

### Product Catalog Management Options

**Traditional — manual entry**
Admin manually adds and edits product records through a config panel. Each product entered field by field.

**Mining from Excel**
On setup, system reads Alex's historical Excel data and extracts every product ever ordered — name, vendor, HCPCS, cost, MSRP — and pre-populates the catalog. Admin reviews and cleans up rather than building from scratch.

**CMS-connected (explored and rejected)**
Pull fee schedule data from CMS public DMEPOS files, eliminating manual maintenance.

*Rejected because:* CMS publishes Medicare reimbursement rates — not Alex's rates. Alex's fee schedule is proprietary: contracted rates per payer that reflect Alex's margin and negotiated agreements. Using CMS rates would collapse the margin structure. Alex's fee schedule is how the business makes money.

---

### Fee Schedule Management Options

**Traditional — manual entry**
Admin manually enters each payer + HCPCS + ZIP + rate row by row. Grows with every new payer, geography, and product.

**Rule-based**
Admin defines rules rather than rows — e.g. "Payer X pays base rate × 1.15 for compression garments in non-rural ZIPs." System computes rates from rules. One rule update cascades to all affected combinations. New products in a category inherit rules automatically.

**ERA/EOB-driven (explored, deferred)**
System learns fee schedule rates from actual insurance payment remittances (ERA/EOB). Self-corrects over time. Not selected for v1 — requires payment history depth and remittance processing infrastructure. Valid for a later stage.

---

## Jobs To Be Done Analysis

### JTBD 1: Enter a patient order correctly without needing to know pricing rules, fee schedules, or vendor logic by heart

| Option | How it handles this JTBD |
|---|---|
| Option 1 — Web App | Employee selects products from catalog dropdown. Pricing auto-populates from fee schedule. System does the lookup — employee doesn't need to know rates. |
| AI-assisted | AI extracts patient info and products from incoming document. Pricing auto-populates. Employee corrects errors and confirms. Employee doesn't need to know rules or product names. |
| Clinic-side Intake | Clinic selects products. When order arrives, pricing is already calculated. Employee reviews pre-filled order — needs to know enough to validate, not enough to construct. |

### JTBD 2: Trust that the system produces consistent output regardless of who processes the order

| Option | How it handles this JTBD |
|---|---|
| Option 1 — Web App | Consistency depends on catalog and fee schedule accuracy. Same inputs always produce same output. Human error only possible at product selection step. |
| AI-assisted | Adds extraction layer with its own consistency risk. If AI misreads document, output is wrong. Employee review is the correction gate. Consistency depends on AI accuracy plus employee vigilance. |
| Clinic-side Intake | Consistency depends on clinic selecting correctly. Employee review must catch clinic mistakes, not just system ones. Introduces an external variable. |

### JTBD 3: Complete order entry without switching between tools, looking up hidden tables, or asking a more experienced colleague

| Option | How it handles this JTBD |
|---|---|
| Option 1 — Web App | Employee stays in web app for entire entry flow. Source document still arrives separately — one tool for entry, one for reference. |
| AI-assisted | Employee stays in one interface. Document forwarded directly to AI. Closest to zero context switching if orders arrive digitally. |
| Clinic-side Intake | Employee only touches review screen. No data entry, no tool switching. Context switching burden shifts upstream to clinic. |

### Management JTBD A: Keep the product catalog accurate and up to date

| Approach | How it handles this JTBD |
|---|---|
| Traditional | Admin manually adds/edits records. Accurate as long as someone is disciplined. Cold-start: built from scratch. |
| Mining | System reads Alex's historical Excel on setup, pre-populates catalog. Admin reviews and cleans up. Accurate from day one because it reflects what Alex has actually ordered. |

### Management JTBD B: Keep the fee schedule accurate and up to date

| Approach | How it handles this JTBD |
|---|---|
| Traditional | Admin manually enters/edits each payer + HCPCS + ZIP + rate row. Maintenance burden grows with every new combination. |
| Rule-based | Admin defines rules, not rows. One update cascades across all affected combinations. New products in a category inherit rules automatically. Scales with rule count, not data point count. |

---

## Option Combinations — Full Ranking

| Rank | Order Entry | Catalog | Fee Schedule | Risk | Innovation | Pros | Cons |
|---|---|---|---|---|---|---|---|
| **1** | Web App | Mining | Rule-based | Low | Medium | Proven order entry — full control, no new tech risk. Mining eliminates cold-start, catalog pre-populated from day one. Rules scale better than rows — one update cascades across all affected combinations. Foundational architecture — API layer supports Stage 2–4 without refactoring. | Rules require upfront thinking to define correctly. If a rule is wrong, errors cascade. Employee still does all data entry manually. |
| **2** | AI-assisted | Mining | Traditional | Medium | Medium | AI reduces manual typing burden — employee reviews instead of types. Mining eliminates cold-start. Platform-agnostic. Traditional fee schedule keeps one variable predictable. | AI extraction accuracy risk on low-quality clinic documents (faxes, handwritten forms). Traditional fee schedule grows as a maintenance burden. AI adds cost and a new failure mode. |
| **3** | Web App | Traditional | Traditional | Very Low | None | Fully proven, no new technology introduced. Simple to build and debug. Every behavior is predictable. | Highest long-term maintenance burden. Cold-start problem — catalog and fee schedule built from scratch. No reduction in employee data entry effort. |
| **4** | AI-assisted | Traditional | Traditional | Medium | Low-Medium | Reduces employee data entry burden. Only one new technology introduced. | Cold-start problem unsolved. Traditional fee schedule is a growing maintenance burden. Pays AI complexity cost without getting data management benefit. |
| **5** | AI-assisted | Mining | Rule-based | Medium | High | Least manual work across the board. Most innovation per component. | Highest complexity — multiple layers that can each fail independently. AI accuracy and rule correctness both require validation simultaneously. Hardest to debug. |
| **6** | Web App | Mining | Traditional | Low | Low | Safe order entry. Mining solves cold-start. Simpler than rule-based. | Traditional fee schedule remains a growing maintenance burden. Misses the biggest ongoing data management improvement. |
| **7** | Clinic-side | Mining | Rule-based | High | High | Most disruptive — eliminates internal data entry if adoption succeeds. Mining and rules reduce maintenance burden. | Clinic adoption is an external dependency Alex cannot control. Creates two-tier problem if some clinics don't adopt. May strain clinic relationship. |

---

## Why Options Were Not Selected

### Why AI-assisted entry was not selected (Rank 2, 4, 5)
AI is a valid option and may be the right evolution in Stage 2. It was not selected for v1 for three reasons:
1. **Risk mismatch:** Clinic documents often arrive as faxed PDFs or handwritten forms — AI extraction accuracy on low-quality, inconsistent sources is meaningfully lower than on clean digital inputs. A wrong HCPCS code or quantity extracted by AI reaches billing, producing a claim error.
2. **Problem mismatch:** Alex never described form-filling speed as a pain. The stated pain was fragile logic and unreliable data. AI-assisted entry solves a problem Alex didn't raise.
3. **Cost and complexity:** AI adds API costs, integration overhead, and a new failure mode — without a proportional benefit in v1 given the above.

### Why Clinic-side intake was not selected (Rank 7)
Conceptually sound but introduces an external dependency Alex cannot control. Clinics may prefer fax or email. Non-adoption creates a two-tier problem where some orders still require full manual entry. Changes the clinic relationship in ways that may create friction. Valid to revisit once the internal system is proven.

### Why Traditional + Traditional was not selected (Rank 3, 4, 6)
Traditional catalog management with traditional fee schedules solves today's problem but not tomorrow's. As payers, geographies, and products grow, the maintenance burden grows proportionally. The architecture doesn't extend cleanly to Stage 2–4 without data migrations and schema changes. Building on a flat lookup table now means more expensive rework later.

### Why Mining alone without Rule-based was not selected (Rank 6)
Mining solves the cold-start problem correctly. But pairing it with a traditional lookup fee schedule means the long-term maintenance problem is deferred, not solved. The same complexity Alex has today — hundreds of payer + HCPCS + ZIP combinations to maintain manually — returns within months of launch as the business grows.

### Why Excel as order entry interface was rejected (not ranked)
Keeps the operational backbone problem alive. Excel has no access controls on patient/billing data, no audit trail, no data integrity constraints, and no surface for future features to live on. Mining and rules engine ideas are sound — keeping Excel as the front-end wastes them and contradicts the root cause we defined.

### Why CMS-connected fee schedules were rejected
CMS publishes Medicare reimbursement rates — not Alex's rates. Alex's fee schedule is proprietary: contracted rates per payer that reflect Alex's margin and negotiated agreements. Alex's fee schedule is how the business makes money.

---

## Selected Recommendation

**Option 1 (Web App) + Mining + Rule-based fee schedule**

### Rationale

**What Alex asked for vs. what Alex needs:**
Alex asked for two tables and a dropdown form — a better Excel. What Alex's business needs is reliable billing accuracy, explicit and auditable business rules, and a foundation the operation can grow on. The selected combination serves the need, not the request.

**Why this is foundational:**
Every decision made in v1 is still the right decision in v3:
- Web interface → Stage 2–4 features (document generation, vendor routing, approval gates) have a home
- API between data and form → AI layer, clinic portal, and document generation can consume the same data later without refactoring
- Rules engine → Adding a new payer or geography is a new rule, not a data migration
- Mining → Data is accurate and complete from day one, not built from scratch

**The principle:**
> Build minimum scope on maximum foundation.

---

## Problems Solved by This Recommendation

**Directly solved:**
- Lack of centralized structured data — canonical database seeded via mining
- Complex pricing logic embedded in spreadsheets — replaced by rule-based engine
- Heavy reliance on tribal knowledge — rules encode what employees carry in their heads
- Fragile spreadsheet logic — replaced by database with integrity constraints
- Excel as operational backbone — replaced by web interface
- High cognitive load on employees — auto-population removes need to know rules

**Not solved — deferred to later stages:**
- Manual re-entry into vendor portals (Stage 2)
- Lack of automated vendor routing (Stage 2)
- Manual document generation (Stage 2)
- HCPCS approval gate enforcement (Stage 3)
- Prior authorization tracking (Stage 3)
- Measurement form uploads (Stage 4)
- Self-pay pricing configuration beyond MSRP (Stage 4)
- Tribal knowledge documentation as process (Stage 4)
