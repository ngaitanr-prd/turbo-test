# Video Presentation Storyboard
**Project:** turbo-test — Alex's Internal Operations Tool
**Format:** Video presentation (screen recording / talking head)
**Runtime estimate:** ~8–12 min depending on pacing
**Audience:** Alex (stakeholder), internal review
**Arc:** Problems → Selection → Solutions → Demo handoff

---

## Presentation Structure at a Glance

| Act | Frames | What it does |
|-----|--------|--------------|
| ACT 1 — The Problem Landscape | 1–6 | Establish the four problems, make them felt, show business impact |
| ACT 2 — The Problem We're Attacking | 7–9 | What / Why / So What for Problem 1 |
| ACT 3 — The Solutions Shootout | 10–15 | 3 solution dimensions, distinct options with pros/cons, chosen combination |
| CLOSE — Handoff to Demo | 16 | Transition to prototype |

---

## ACT 1 — The Problem Landscape

---

### FRAME 1 — Hook / Title

**Headline (on screen):**
> "Before we build anything — let's name what's actually broken."

**Visual:** Dark background. Single sentence. No logo, no decoration.
White text, large. Pause 2 seconds before narration begins.

**Narration:**
> "Alex runs a medical supply distribution business. Small team, complex operation — insurance verification, prior authorizations, vendor ordering, billing. And right now, all of it lives inside a single Excel spreadsheet. We spent time understanding what's actually wrong. And it turns out there aren't ten problems. There are four."

**Design notes:**
- Cinematic open — no fluff, no agenda slide
- Black or very dark navy background
- Helvetica or Inter, white, 48–60pt
- 2-second beat of silence before voice starts

---

### FRAME 2 — The Four Problems Overview

**Headline:**
> "Four problems. Four different roots."

**Visual:** 2×2 grid. Each quadrant = one problem.
Each card: number (large, bold, accent color) + short name + 1-line type label.

```
┌─────────────────────┬─────────────────────┐
│   P1                │   P2                │
│   No Reliable       │   People Are        │
│   Master Data       │   the Middleware    │
│   [Data problem]    │   [Integration      │
│                     │    problem]         │
├─────────────────────┼─────────────────────┤
│   P3                │   P4                │
│   Compliance        │   Critical          │
│   Controls Outside  │   Knowledge in      │
│   the Workflow      │   People's Heads    │
│   [Governance       │   [Knowledge        │
│    problem]         │    problem]         │
└─────────────────────┴─────────────────────┘
```

**Narration:**
> "We identified four genuinely distinct problems. Not variations on a theme — each one has a different root, requires a different type of fix, and sits in a sequence. Let me walk through each one."

**Design notes:**
- Cards appear one at a time (animated reveal) as narrator mentions each
- Accent color per quadrant: warm orange, electric blue, amber, teal
- Type label in small caps, subdued color
- Grid layout should feel like a 2×2 matrix, not a bullet list

---

### FRAME 3 — Problem 1: No Reliable Master Data

**Headline:**
> "P1 — The pricing data doesn't exist in one trusted place."

**Visual:** Left column: problem description card. Right column: business impact visual.

**Left — Problem card:**
> Product costs, fee schedules, pricing rules, and payer rates live in hidden Excel tables and people's memory. There's no single source to look something up and trust the answer.

**Right — Impact visual (use an icon + short sharp statement):**
```
💸 Two employees process the same order →
   two different prices
   two different margins
   two different patient balances
```

**Narration:**
> "Problem one: the master data doesn't reliably exist. Pricing rules, fee schedules, payer rates — they live in hidden Excel formulas and in people's heads. The consequence is direct: two people processing the same order produce two different prices, different margins, different patient balances. And any automation you build on top of this data inherits every mistake already in it."

**Design notes:**
- P1 card highlighted (glowing border) — this is the problem we're attacking
- Impact visual uses a simple branching arrow: "same order → two outcomes"
- Keep impact statement punchy, not exhaustive

---

### FRAME 4 — Problem 2: People Are the Middleware

**Headline:**
> "P2 — A person bridges every gap between systems."

**Visual:** Left: problem card. Right: simple flow diagram showing manual handoffs.

**Left — Problem card:**
> After an order is captured, the team re-enters it manually into vendor portals, assembles PDFs by hand, and routes by email. Every system is disconnected. A person bridges each gap.

**Right — Flow visual:**
```
Order captured
      ↓
  [Person] — re-types into vendor portal
      ↓
  [Person] — assembles PDF by hand
      ↓
  [Person] — routes by email
      ↓
  Billing
```

**Business impact tag:**
> "Throughput has a ceiling. Scaling the business requires proportional headcount growth."

**Narration:**
> "Problem two: people are the middleware. Once an order is in the system, a human being re-enters it into the vendor portal, assembles documents by hand, and routes by email. Every system is disconnected. You can't scale the business without scaling the headcount doing this work."

**Design notes:**
- Flow shows clear manual intervention at each step
- Use person icon (circle-head figure) at each manual step
- Muted colors for this problem — not the one we're attacking now

---

### FRAME 5 — Problem 3 & 4

**Headline:**
> "P3 & P4 — Compliance controls exist but aren't enforced. Critical rules aren't written down."

**Visual:** Split screen, two compact cards side by side.

**P3 card:**
> The HCPCS approval gate lives in SharePoint — outside the order flow. It can be skipped. Prior auth requirements are tracked in experienced employees' heads.
>
> **Impact:** Approvals can be bypassed. Prior auth gets missed. Claim denials, audit exposure, no paper trail.

**P4 card:**
> Vendor routing logic, prior auth rules, product exceptions, pricing edge cases — none of it is written anywhere the system can read.
>
> **Impact:** Onboarding takes months. Decisions are inconsistent. When someone leaves, the knowledge leaves with them.

**Narration:**
> "Problems three and four are compliance and knowledge. In P3, the rules *exist* — the approval gate lives in SharePoint — but nothing enforces them inside the order flow. In P4, the rules don't even exist in writing. Prior auth requirements and vendor routing logic live only in experienced employees' heads. These are sequenced problems — they come after we fix the foundation."

**Design notes:**
- Both cards muted — these are real but deferred
- Fine-print label under each: "Stage 3" / "Stage 4"
- Keep this frame moving — two problems on one slide signals they're not today's focus

---

### FRAME 6 — Business Impact Summary

**Headline:**
> "Same root symptom, four different failure modes."

**Visual:** A 2-column table, clean and readable.

| Problem | What breaks in Alex's business |
|---------|-------------------------------|
| P1 — No Master Data | Prices vary by who processes the order. Errors cascade into billing and reimbursement. |
| P2 — People as Middleware | Operational ceiling hit. Growth requires more staff doing the same manual steps. |
| P3 — Governance Gap | Approvals get skipped. Prior auth missed. Audit exposure with no paper trail. |
| P4 — Knowledge in Heads | Onboarding is slow. Decisions are inconsistent. Key-person risk. |

**Narration:**
> "What Alex has is not a tech problem — it's four compounding operational failure modes. The business works today because experienced people are carrying it. But it can't scale, it can't self-correct, and it can't be audited. We need to fix this in sequence, starting at the root."

**Design notes:**
- Table rows animate in one at a time
- P1 row highlighted — it's the one we're here to address
- End this frame with a visual cue transitioning to Act 2: "So — which one do we attack first?"

---

## ACT 2 — The Problem We're Attacking

---

### FRAME 7 — The What

**Headline:**
> "WHAT — No reliable master data."

**Visual:** Large central statement with three supporting bullets.

**Central statement (large, bold):**
> Alex's team has no single place to look up product data and trust the answer.

**Three bullets below:**
- Product costs → scattered across hidden Excel tables
- Fee schedules → embedded in opaque formulas
- Pricing rules → stored in experienced employees' heads

**Narration:**
> "Here's the problem we're attacking first. There is no reliable canonical source for product and pricing data. Product costs, fee schedules, payer rates — they live in hidden Excel tables, opaque formulas, and people's memory. The same information exists in multiple places, with no guarantee any of them agree."

**Design notes:**
- Clean, minimal frame — big central statement owns the space
- Three bullets use a subtle "source" icon (document, formula, person) to differentiate each
- Accent color on "WHAT" label (top left or header)

---

### FRAME 8 — The Why

**Headline:**
> "WHY first — it's a prerequisite, not a priority."

**Visual:** Dependency map / unlock tree.

```
                    ┌──────────────────────────┐
                    │  P1: No Reliable         │
                    │  Master Data  ← FIXING   │
                    └──────────────┬───────────┘
                                   │ unlocks
          ┌────────────────────────┼────────────────────────┐
          ▼                        ▼                        ▼
 ┌──────────────────┐   ┌──────────────────┐   ┌──────────────────┐
 │ Automate vendor  │   │ Auto-populate    │   │ Track prior auth  │
 │ routing safely   │   │ pricing in forms │   │ requirements     │
 └──────────────────┘   └──────────────────┘   └──────────────────┘
          ▼                        ▼
 ┌──────────────────┐   ┌──────────────────┐
 │ Enforce HCPCS    │   │ Generate docs    │
 │ approval gates   │   │ correctly        │
 └──────────────────┘   └──────────────────┘
```

**Narration:**
> "We're not attacking this problem first because it's the highest ROI in isolation. We're attacking it first because nothing else is safe to build without it. You cannot reliably automate vendor routing if vendor rules aren't written down. You cannot auto-populate pricing if the pricing logic is opaque. You cannot track prior auth if no one has codified which products need it. Automating on top of scattered data doesn't solve the problem — it propagates errors faster."

**Design notes:**
- Dependency tree builds as narrator speaks — each unlocked item appears
- P1 node glows or pulses at top
- Five dependent nodes appear progressively — visual weight shows what we're unlocking

---

### FRAME 9 — The So What

**Headline:**
> "SO WHAT — We attack the root. Not the symptoms."

**Visual:** Before / After split.

**BEFORE (left, muted, slightly chaotic visual):**
- Hidden Excel tables → errors cascade into every order
- Two people, same order → different price, different margin
- Automation on bad data → faster wrong answers
- Adding new payers → manually updating every combination

**AFTER (right, clean, confident visual):**
- One canonical database → every order, every person, same answer
- New payer or product → one update, cascades everywhere
- Automation is trustworthy → because the data underneath it is
- Stages 2–4 have a foundation to build on

**Narration:**
> "So what does solving this actually mean for Alex's business? Before: hidden tables, diverging prices, errors baked into every order. After: one trusted source for all product and pricing data — every order, every employee, every time. And critically: every feature we build in Stage 2 through 4 has a reliable foundation to stand on instead of inheriting the same broken data."

**Design notes:**
- Use visual contrast: left side has visual noise (overlapping sheets, diverging arrows), right side is clean and structured
- Transition animation from left to right feels like "clearing the fog"
- End this frame on the AFTER side — let it breathe before moving to solutions

---

## ACT 3 — The Solutions Shootout

---

### FRAME 10 — Three Dimensions

**Headline:**
> "The solution has three moving parts. We evaluated each independently."

**Visual:** Three horizontal lanes, each with a label.

```
┌─────────────────────────────────────────────────────────┐
│  DIMENSION 1: Order Entry                               │
│  How does an employee capture an order?                 │
├─────────────────────────────────────────────────────────┤
│  DIMENSION 2: Catalog Management                        │
│  How does product data get into the system?             │
├─────────────────────────────────────────────────────────┤
│  DIMENSION 3: Fee Schedule Management                   │
│  How does pricing logic get into the system?            │
└─────────────────────────────────────────────────────────┘
```

**Narration:**
> "The solution we're building has three components: an order entry experience, a product catalog, and a fee schedule. We brainstormed fundamentally different approaches to each — not just tech variations, but architecturally different ways to solve each dimension. Let me walk through the real options."

**Design notes:**
- Three lanes feel like a product board — structured, not a bullet list
- Each lane gets a distinct icon (form, catalog/book, rule engine)
- This frame is a nav map — audience knows what's coming

---

### FRAME 11 — Dimension 1: Order Entry Options

**Headline:**
> "Order Entry — Three fundamentally different approaches."

**Visual:** Three option cards side by side, with a verdict badge on the chosen one.

**Option A: Web App**
> Employee opens a structured web form, selects products from a catalog dropdown. System auto-populates HCPCS, pricing, and billing fields. Employee reviews and submits.
>
> ✅ Full control over data integrity
> ✅ Proven — no new technology risk
> ✅ Foundation for Stage 2–4 features
> ❌ Employee still does all manual entry

**Option B: AI-Assisted Entry**
> AI reads an incoming clinic document (fax, email, PDF), extracts patient info and products, pre-fills the form. Employee reviews and corrects.
>
> ✅ Reduces typing burden significantly
> ✅ Platform-agnostic
> ❌ AI accuracy lower on faxed / handwritten forms
> ❌ Wrong HCPCS extracted → billing error
> ❌ Solves a pain Alex never raised

**Option C: Clinic-Side Intake**
> Clinic fills a structured form directly in a portal Alex provides. Structured data arrives pre-priced. Employee reviews and approves.
>
> ✅ Least internal manual entry
> ✅ Most disruptive if adopted
> ❌ External dependency Alex cannot control
> ❌ Creates two-tier problem if some clinics don't adopt
> ❌ Changes the clinic relationship

**Verdict badge on Option A:** ✓ SELECTED

**Narration:**
> "For order entry, we looked at three genuinely different approaches. A structured web app — the safest, most predictable option. AI-assisted entry where the AI reads incoming clinic documents and pre-fills the form. And a clinic-side intake portal where the clinic does the data entry directly. Each option serves a different vision of who does the work. Here's why AI was compelling but rejected: clinic documents often arrive as faxed PDFs or handwritten forms. AI extraction accuracy on those is meaningfully lower than on clean digital inputs. One wrong HCPCS code extracted reaches billing and becomes a claim error. And critically — Alex never said form-filling speed was the pain. The pain was bad data. AI solves the wrong problem. Clinic-side intake is architecturally exciting but introduces an external dependency Alex can't control. Web app wins."

**Design notes:**
- Three cards with equal visual weight initially — no winner telegraphed upfront
- Build tension: narration goes through pros/cons before revealing verdict
- Verdict badge appears last on Option A — satisfying reveal
- Rejected options get subtle visual dimming / strikethrough, not erasure — audience should see WHY they were considered

---

### FRAME 12 — Dimension 2: Catalog Management Options

**Headline:**
> "Catalog Management — Cold start is the real problem."

**Visual:** Two option cards (+ one rejected option, shown but crossed out).

**Option A: Traditional Manual Entry**
> Admin manually adds and edits product records through a config panel. Each product entered field by field.
>
> ✅ Simple, predictable
> ✅ Admin controls every record
> ❌ Cold start: built from scratch (months of work)
> ❌ No reduction in initial setup burden

**Option B: Mining from Excel**
> On setup, system reads Alex's historical Excel data and extracts every product ever ordered — name, vendor, HCPCS, cost, MSRP. Pre-populates the catalog. Admin reviews and cleans up, not builds from scratch.
>
> ✅ Catalog is accurate from day one
> ✅ Reflects what Alex has actually ordered, not theoretical products
> ✅ Admin reviews and confirms rather than builds
> ❌ Requires a clean-enough Excel to mine from

**Rejected — CMS-Connected (shown crossed out):**
> Pull fee schedule data from public CMS DMEPOS files.
> ✗ CMS publishes Medicare rates — not Alex's contracted rates. Alex's fee schedule *is* the margin. Using CMS rates would collapse it.

**Verdict badge on Option B:** ✓ SELECTED

**Narration:**
> "For the product catalog, the key tension is the cold-start problem. Do you build the catalog from scratch, or can you seed it? Mining solves this elegantly — the system reads Alex's historical Excel data on setup and extracts every product the business has ever ordered. The catalog arrives pre-populated. Admin cleans it up rather than constructing it. We also explored pulling from CMS public data — but CMS publishes Medicare reimbursement rates, not Alex's contracted rates. Alex's fee schedule is how the business makes money. Using CMS rates would destroy the margin structure."

**Design notes:**
- CMS option shown visually as "crossed out" with brief label explaining why
- Mining option gets visual: Excel icon → arrow → clean catalog → admin with checkmark
- Emphasize the cold-start problem visually: "start from zero" vs "start from your own history"

---

### FRAME 13 — Dimension 3: Fee Schedule Options

**Headline:**
> "Fee Schedule — Rows don't scale. Rules do."

**Visual:** Two option cards side by side, with a scale visualization.

**Option A: Traditional Manual (Flat Lookup)**
> Admin manually enters each payer + HCPCS + ZIP + rate row by row. One row per combination.
>
> ✅ Simple to understand
> ✅ No abstraction overhead
> ❌ Grows proportionally with every new payer, geography, product
> ❌ Update one rate → update every row it affects manually
> ❌ Same problem Alex has today, slightly better organized

**Option B: Rule-Based Engine**
> Admin defines rules, not rows. "Payer X pays base rate × 1.15 for compression garments in non-rural ZIPs." System computes rates from rules. One rule update cascades to all affected combinations. New products in a category inherit rules automatically.
>
> ✅ One update cascades across all affected combinations
> ✅ New products in a category inherit rules automatically
> ✅ Scales with rule count, not data point count
> ❌ Rules require upfront thinking to define correctly
> ❌ A wrong rule cascades its error too

**Scale visual (side by side):**
```
Traditional          Rule-based
─────────────        ─────────────
Year 1: 50 rows      Year 1: 5 rules
Year 2: 200 rows     Year 2: 8 rules
Year 3: 800 rows     Year 3: 12 rules
        ↑ grows                ↑ manageable
        exponentially
```

**Deferred option (shown, not selected):**
> ERA/EOB-Driven: system learns rates from actual insurance payment remittances. Self-corrects over time. Deferred — requires payment history depth and remittance processing infrastructure. Valid for Stage 3.

**Verdict badge on Option B:** ✓ SELECTED

**Narration:**
> "The fee schedule is where the most important architectural decision hides. Traditional lookup tables — flat rows of payer, HCPCS, ZIP, rate — are simple to understand but they scale with the data. Year one you have 50 rows. Year two, 200. Year three, 800. Every new payer, geography, or product multiplies the maintenance burden. Rule-based flips this: you define a rule, not a row. One rule update cascades to every combination it affects. New products in a category inherit the rule. The maintenance burden scales with rule count, not data point count. We also considered ERA/EOB-driven learning — where the system infers rates from actual insurance payment remittances. Elegant, but it needs payment history depth we don't have yet. Deferred to Stage 3."

**Design notes:**
- The scaling visual is the hero of this frame — make it prominent
- Rows growing exponentially vs rules staying manageable — use a bar chart or simple count list
- ERA/EOB shown in lighter text as "future" not "rejected"

---

### FRAME 14 — The Chosen Combination

**Headline:**
> "The recommendation: Web App + Mining + Rule-based fee schedule."

**Visual:** Three columns, each confirming the chosen option per dimension. Below: the design principle.

```
ORDER ENTRY          CATALOG              FEE SCHEDULE
──────────────       ──────────────       ──────────────
✓ Web App            ✓ Mining             ✓ Rule-based
  Employee enters      Pre-seeded from      Rules, not rows
  from structured      Alex's history       One rule updates
  form. Pricing                             everything
  auto-populated.
```

**Design principle (large, centered below):**
> "Build minimum scope on maximum foundation."

**Below the principle:**
> Every decision made in v1 is still the right decision in v3.
> - Web interface → future features (docs, vendor routing, approvals) have a home
> - API layer → AI, clinic portal, document generation can plug in later without refactoring
> - Rules engine → new payer or geography = new rule, not a data migration
> - Mining → data is accurate from day one, not built from scratch

**Narration:**
> "Put it together: Web App for order entry, Mining to seed the catalog, Rule-based engine for the fee schedule. This isn't just a practical combination — it's a foundational one. Every decision we're making in version one is still the right decision in version three. The web interface gives Stage 2–4 features a home. The API layer means AI-assisted entry or a clinic portal can plug in later without refactoring the core. The rules engine means adding a new payer or geography is a new rule, not a migration. Mining means the data is accurate from day one. Build minimum scope on maximum foundation."

**Design notes:**
- Three columns animate in, then the design principle drops in below with weight
- The principle line gets a visual emphasis: large font, maybe a line above and below
- "Every decision made in v1 is still the right decision in v3" should feel like a headline, not a footnote

---

### FRAME 15 — What This Solves (and What It Doesn't)

**Headline:**
> "What this fixes now — and what we're building toward."

**Visual:** Two-column layout.

**Directly solved (left — lit up, confident):**
- Lack of centralized structured data ✓
- Complex pricing logic embedded in spreadsheets ✓
- Fragile spreadsheet logic ✓
- Excel as operational backbone ✓
- High cognitive load on employees ✓
- Heavy reliance on tribal knowledge (partial) ✓

**Deferred — later stages (right — muted, future-tense):**
- Manual re-entry into vendor portals → Stage 2
- Automated vendor routing → Stage 2
- Manual document generation → Stage 2
- HCPCS approval gate enforcement → Stage 3
- Prior authorization tracking → Stage 3
- Measurement form uploads → Stage 4

**Narration:**
> "Here's what this effort directly fixes: no more scattered pricing data, no more opaque spreadsheet formulas, no more Excel as the operational backbone. And problems two through four — the integration, governance, and knowledge problems — are explicitly deferred, not forgotten. They're sequenced after this foundation because without it, they can't be built safely. Now let me show you what this actually looks like."

**Design notes:**
- Left column: bright, checkmarks animate in — satisfying
- Right column: muted, "→ Stage X" labels suggest forward motion, not abandonment
- Last sentence of narration is the pivot to demo — pause here, let it land

---

## CLOSE — Handoff to Demo

---

### FRAME 16 — Transition to Prototype

**Headline:**
> "Let's look at it."

**Visual:** Minimal. Dark background. Single line. Possibly a blurred preview of the prototype behind the text.

**Narration:**
> "Everything you just heard — the catalog, the fee schedule, the order entry form — we built a prototype. Let me walk you through it."

**Design notes:**
- Cinematic close mirrors the cinematic open
- No bullets, no agenda, no "in summary"
- "Let's look at it." — four words. Confident. Stops talking, starts showing.
- Fade to demo screen or screen share

---

## Appendix: Speaker Pacing Notes

| Frame | Approx. time | Pacing note |
|-------|-------------|-------------|
| 1 | 20 sec | Slow, let the hook land |
| 2 | 30 sec | Animated reveal — let each card appear with a beat |
| 3 | 45 sec | P1 is the hero — give it space |
| 4 | 40 sec | Flow visual does the work — less narration needed |
| 5 | 35 sec | Fast — these are deferred, signal that |
| 6 | 30 sec | Summary frame — move through it |
| 7 | 40 sec | Clean, clear — don't rush the WHAT |
| 8 | 60 sec | The unlock tree needs time — this is the core argument |
| 9 | 45 sec | Before/after contrast — let AFTER breathe |
| 10 | 20 sec | Nav frame — quick, just orient the audience |
| 11 | 90 sec | Build tension across 3 options before revealing verdict |
| 12 | 60 sec | Cold-start is the key insight here |
| 13 | 75 sec | Scaling visual is the hero — let it land |
| 14 | 60 sec | Principle drop is the moment — pause after it |
| 15 | 45 sec | Pivot line at the end — crisp and confident |
| 16 | 10 sec | Four words. Stop. Demo. |
| **Total** | **~9 min** | At comfortable video pace |

---

## Appendix: Visual Language Spec

| Element | Spec |
|---------|------|
| Background | Near-black (#0F0F13) or very dark navy |
| Primary text | White (#FFFFFF) |
| Headlines | 48–60pt, Inter or Helvetica, Bold |
| Body / bullets | 22–26pt, Inter Regular |
| Accent colors | P1: Electric blue (#3B82F6), P2: Amber (#F59E0B), P3: Orange (#EF4444), P4: Teal (#14B8A6) |
| Chosen option badge | Green (#22C55E), bold checkmark |
| Rejected / deferred | 40% opacity, no color saturation |
| Animation style | Fade + slight upward drift. No bounce. No spin. |
| Transitions between frames | Cross-fade, 0.3s |
| Video aspect ratio | 16:9 |
