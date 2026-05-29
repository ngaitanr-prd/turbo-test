# Slide Deck — Alex's Internal Operations Tool
**Format:** Pitch Deck / Slide Deck hybrid · Video-ready
**16 slides · 3 acts**

---

## How to read this file

Each slide block contains:
- **HEADLINE** — the large text at the top of the slide (the message, not a label)
- **BODY** — exactly what appears on the slide
- **LAYOUT** — how to arrange the elements
- **SPEAKER CUE** — one line for you (not on the slide)

---
---

# ACT 1 — THE PROBLEM LANDSCAPE

---

## SLIDE 1 — Title / Hook

---

**HEADLINE (full-slide, centered):**
```
Before we build anything —
let's name what's actually broken.
```

**BODY:** *(nothing else — headline only)*

**LAYOUT:** Full bleed dark background. Headline centered, large (60–72pt). No logo, no subtitle, no agenda. White text on near-black.

**SPEAKER CUE:** Open in silence for 2 seconds, then start talking.

---

## SLIDE 2 — The Four Problems

---

**HEADLINE:**
```
Four problems. Four different roots.
```

**BODY — 2×2 grid of cards:**

| | |
|---|---|
| **P1** · No Reliable Master Data · *Data problem* | **P2** · People Are the Middleware · *Integration problem* |
| **P3** · Compliance Controls Outside the Workflow · *Governance problem* | **P4** · Critical Knowledge in People's Heads · *Knowledge problem* |

**LAYOUT:** 2×2 grid. Each card: problem number (large, bold, accent color) + name + italicized type label below. Cards equal size. P1 gets a subtle highlight border — it's the one we're here for.

**SPEAKER CUE:** "Each one has a different root and requires a different fix. They're also sequenced."

---

## SLIDE 3 — Problem 1

---

**HEADLINE:**
```
P1 — No single place to look up pricing and trust the answer.
```

**BODY — two columns:**

**Left — What's happening:**
> Product costs, fee schedules, pricing rules, and payer rates live in hidden Excel tables and people's memory.

**Right — What it means for Alex:**

| Same order, two employees |
|---|
| → Two different prices |
| → Two different margins |
| → Two different patient balances |

> Any automation built on top of this data inherits every mistake already in it.

**LAYOUT:** Left column: problem statement (body text, ~24pt). Right column: branching visual or simple 3-row table with arrow. Right column is the emotional punch — give it visual weight.

**SPEAKER CUE:** This is the problem we're solving. Let it land.

---

## SLIDE 4 — Problem 2

---

**HEADLINE:**
```
P2 — A person bridges every gap between systems.
```

**BODY — Left: description. Right: flow diagram.**

**Left:**
> After an order is captured, the team re-enters it manually into vendor portals, assembles PDFs by hand, and routes by email. Every system is disconnected.

**Right — flow:**
```
Order received
      ↓
 👤 Re-types into vendor portal
      ↓
 👤 Assembles PDF by hand
      ↓
 👤 Routes by email
      ↓
   Billing
```

**Bottom tag (full width):**
> **Scaling the business requires proportional headcount growth to do the same manual steps.**

**LAYOUT:** 50/50 split. Flow diagram on right uses person icon at each manual step. Bottom callout bar spans full width — contrasting background color.

**SPEAKER CUE:** This is Stage 2. Move through it — it's real but not today's problem.

---

## SLIDE 5 — Problems 3 & 4

---

**HEADLINE:**
```
P3 & P4 — Controls that can be skipped. Rules that aren't written down.
```

**BODY — two equal cards:**

**P3 — Governance problem:**
> The HCPCS approval gate lives in SharePoint — outside the order flow. It can be bypassed. Prior auth requirements live in employees' heads.
>
> **Result:** Approvals get skipped. Prior auth missed. No audit trail.

**P4 — Knowledge problem:**
> Vendor routing logic, prior auth rules, pricing exceptions — none of it is written anywhere the system can use.
>
> **Result:** Onboarding takes months. Decisions are inconsistent. When someone leaves, the knowledge leaves.

**Bottom labels (under each card):**
P3 → *Stage 3*  ·  P4 → *Stage 4*

**LAYOUT:** Two equal cards side by side. Both slightly muted — they're real, not today's focus. Stage labels in small caps at the bottom.

**SPEAKER CUE:** Two problems, one slide — signals they're sequenced after we fix the foundation.

---

## SLIDE 6 — Business Impact Summary

---

**HEADLINE:**
```
Same symptom, four different failure modes.
```

**BODY — table:**

| Problem | What breaks in Alex's business |
|---|---|
| **P1 — No Master Data** | Prices vary by who processes the order. Errors cascade into billing and reimbursement. |
| **P2 — People as Middleware** | Growth requires more staff doing the same manual steps. Throughput hits a ceiling. |
| **P3 — Governance Gap** | Approvals get skipped. Prior auth missed. Audit exposure with no paper trail. |
| **P4 — Knowledge in Heads** | Onboarding is slow. Decisions are inconsistent. Key-person risk. |

**Bottom callout:**
> The business works today because experienced people are carrying it. It can't scale, self-correct, or be audited.

**LAYOUT:** Clean 2-column table. P1 row highlighted (colored left border or row background). Bottom callout in a slightly contrasting card below the table.

**SPEAKER CUE:** This is the "so why fix it" frame. End it with: "We need to fix this in sequence, starting at the root."

---
---

# ACT 2 — THE PROBLEM WE'RE ATTACKING

---

## SLIDE 7 — WHAT

---

**HEADLINE:**
```
WHAT
Alex's team has no single place to look up product
data and trust the answer.
```

**BODY — three items with source icons:**

| Source | What lives there |
|---|---|
| 📄 Hidden Excel tables | Product costs and MSRP |
| ƒ Opaque formulas | Fee schedule logic and payer rates |
| 🧠 Experienced employees | Pricing rules, exceptions, edge cases |

**Bottom line:**
> The same information exists in multiple places, with no guarantee any of them agree.

**LAYOUT:** Headline takes top 40% of slide (large, bold). Three-row table below with icon column. Bottom line in italics, centered.

**SPEAKER CUE:** Simple, declarative. Don't rush it.

---

## SLIDE 8 — WHY

---

**HEADLINE:**
```
WHY FIRST
It's not a priority. It's a prerequisite.
```

**BODY — dependency tree:**

```
         ┌──────────────────────────────┐
         │  P1: No Reliable Master Data │  ← fixing this
         └──────────┬───────────────────┘
                    │ unlocks
     ┌──────────────┼──────────────┬─────────────────┐
     ▼              ▼              ▼                  ▼
Automate      Auto-populate   Track prior        Enforce HCPCS
vendor        pricing in      auth               approval
routing       forms           requirements       gates
```

**Bottom callout:**
> Automating on top of scattered data doesn't solve the problem — it propagates errors faster.

**LAYOUT:** Dependency tree centered on slide. P1 node at top, clearly labeled as "fixing this." Four unlocked nodes branch below — they appear dimmed/future-tense. Bottom callout spans full width.

**SPEAKER CUE:** This is the core argument. The tree does the work — let it breathe.

---

## SLIDE 9 — SO WHAT

---

**HEADLINE:**
```
SO WHAT
We attack the root — not the symptoms.
```

**BODY — Before / After split:**

| BEFORE | AFTER |
|---|---|
| Prices vary by who processes the order | Same inputs → same output, every time |
| Pricing logic lives in hidden formulas | Rules live in the system, auditable |
| Adding a new payer = updating dozens of rows | Adding a new payer = one rule update |
| Automation amplifies existing errors | Automation is trustworthy |
| Stages 2–4 would inherit broken data | Stages 2–4 have a reliable foundation |

**LAYOUT:** Two-column table, "BEFORE" header in muted red/amber, "AFTER" header in green. Row items contrast visually. BEFORE column should feel slightly cramped; AFTER clean and spacious.

**SPEAKER CUE:** End on the AFTER column. Let it sit before moving to solutions.

---
---

# ACT 3 — THE SOLUTIONS SHOOTOUT

---

## SLIDE 10 — Three Dimensions

---

**HEADLINE:**
```
The solution has three moving parts.
We evaluated each independently.
```

**BODY — three horizontal lanes:**

| | Dimension | Question it answers |
|---|---|---|
| 📝 | **Order Entry** | How does an employee capture an order? |
| 📚 | **Catalog Management** | How does product data get into the system? |
| ⚙️ | **Fee Schedule Management** | How does pricing logic get into the system? |

**LAYOUT:** Three horizontal lanes (rows), icon on left, dimension name bold, question in regular weight. This is a navigation frame — clean, fast, no decoration.

**SPEAKER CUE:** Quick frame. Orient the audience, then move.

---

## SLIDE 11 — Order Entry Options

---

**HEADLINE:**
```
Order Entry — Three fundamentally different approaches.
```

**BODY — three option cards:**

| | Option A: Web App | Option B: AI-Assisted | Option C: Clinic-Side Intake |
|---|---|---|---|
| **How it works** | Employee opens a form, selects products from a dropdown. Pricing auto-populates. Employee reviews and submits. | AI reads an incoming clinic document (fax, PDF, email), extracts data, pre-fills the form. Employee reviews and corrects. | Clinic fills a structured intake form directly. Structured data arrives in Alex's system pre-priced. Employee approves. |
| ✅ **Pros** | Full data control · No new tech risk · Foundation for future features | Reduces typing burden · Platform-agnostic | Least internal effort · Most disruptive if adopted |
| ❌ **Cons** | Employee still does all entry manually | AI accuracy drops on faxed/handwritten forms · Wrong HCPCS → billing error · Solves a pain Alex didn't raise | External dependency Alex can't control · Two-tier problem if clinics don't adopt |
| **Status** | ✅ **SELECTED** | Deferred → Stage 2 | Revisit after internal system is proven |

**LAYOUT:** Three equal-width columns. Status row at bottom — Option A gets a green "SELECTED" badge. Options B and C get "Deferred" labels (not "rejected" — they're real candidates for later). Reveal all three first, then badge appears.

**SPEAKER CUE:** Build tension — walk through each option before the badge appears.

---

## SLIDE 12 — Catalog Management Options

---

**HEADLINE:**
```
Catalog Management — The cold-start problem.
```

**BODY — two option cards:**

| | Option A: Traditional Manual Entry | Option B: Mining from Excel |
|---|---|---|
| **How it works** | Admin manually adds and edits product records field by field through a config panel. | On setup, the system reads Alex's historical Excel data and extracts every product ever ordered. Admin reviews and confirms. |
| ✅ **Pros** | Simple · Admin controls every record | Catalog is accurate from day one · Reflects actual orders, not theoretical products · Admin reviews, not builds |
| ❌ **Cons** | Cold start: built from scratch · Months of setup work before the system is useful | Requires a clean-enough Excel source to mine from |
| **Status** | ❌ Higher setup burden | ✅ **SELECTED** |

**Bottom note (separate visual element):**
> **Also evaluated — CMS-connected:** Pull rates from public CMS DMEPOS files.
> **Rejected:** CMS publishes Medicare rates, not Alex's contracted rates. Alex's fee schedule *is* the margin structure. Using CMS rates would collapse it.

**LAYOUT:** Two-column card layout. CMS note at the bottom in a distinct callout box (strikethrough on "CMS-connected" label, short explanation).

**SPEAKER CUE:** The cold-start insight is the key — make sure it lands.

---

## SLIDE 13 — Fee Schedule Options

---

**HEADLINE:**
```
Fee Schedule — Rows don't scale. Rules do.
```

**BODY — two option cards + scale comparison:**

| | Option A: Traditional Lookup | Option B: Rule-Based Engine |
|---|---|---|
| **How it works** | Admin manually enters each payer + HCPCS + ZIP + rate, row by row. One row per combination. | Admin defines rules, not rows. "Payer X pays base rate × 1.15 for compression garments in non-rural ZIPs." System computes rates from rules. |
| ✅ **Pros** | Simple to understand · No abstraction overhead | One update cascades to all affected combinations · New products inherit category rules · Scales with rule count, not data point count |
| ❌ **Cons** | Grows with every new payer, geography, product · Updating one rate = manually updating every row it affects | Rules require upfront definition · A wrong rule cascades its error too |
| **Status** | ❌ Same problem, slightly better organized | ✅ **SELECTED** |

**Scale visual (below the cards):**

```
           Traditional                    Rule-Based
           ────────────                   ──────────
Year 1:    50 rows                        5 rules
Year 2:    200 rows                       8 rules
Year 3:    800 rows  ← grows fast         12 rules  ← stays manageable
```

**Bottom note:**
> **ERA/EOB-Driven (evaluated, deferred):** System learns rates from actual insurance payment remittances. Elegant — but requires payment history depth and remittance infrastructure. Valid for Stage 3.

**LAYOUT:** Two-column cards. Scale visual below cards — this is the hero of the slide, give it visual weight. ERA/EOB note in a small deferred callout at the bottom.

**SPEAKER CUE:** The scaling numbers tell the story — let the visual do the work.

---

## SLIDE 14 — The Chosen Combination

---

**HEADLINE:**
```
The recommendation:
Web App + Mining + Rule-based fee schedule.
```

**BODY — three confirmation columns:**

| ORDER ENTRY | CATALOG | FEE SCHEDULE |
|---|---|---|
| ✅ Web App | ✅ Mining | ✅ Rule-based |
| Employee enters from structured form · Pricing auto-populates | Pre-seeded from Alex's own history · Admin reviews, not builds | Rules, not rows · One update cascades everywhere |

**Design principle (large, centered, below the columns):**
```
"Build minimum scope on maximum foundation."
```

**Below the principle — four bullets:**
- Web interface → future features (docs, vendor routing, approval gates) have a home
- API layer → AI entry, clinic portal, and document generation plug in later without refactoring
- Rules engine → adding a payer or geography = a new rule, not a data migration
- Mining → data is accurate from day one, not built from scratch

**LAYOUT:** Three-column header. Design principle as a blockquote or pull quote — large font, centered, visually dominant. Four bullets below in two columns or a single column, smaller text.

**SPEAKER CUE:** The principle is the moment — pause after it lands.

---

## SLIDE 15 — What This Solves (and What It Doesn't)

---

**HEADLINE:**
```
What this fixes now — and what comes next.
```

**BODY — two-column layout:**

**FIXED NOW ✅**
- No more scattered product and pricing data
- No more opaque spreadsheet formulas
- No more Excel as the operational backbone
- Order entry is consistent regardless of who processes it
- Pricing auto-populates — employees don't need to carry rules in their heads

**COMING NEXT →**
- Manual re-entry into vendor portals → *Stage 2*
- Automated vendor routing → *Stage 2*
- Manual document generation → *Stage 2*
- HCPCS approval gate enforcement → *Stage 3*
- Prior authorization tracking → *Stage 3*

**Bottom callout:**
> Problems 2, 3, and 4 are documented and sequenced — not forgotten.

**LAYOUT:** Two columns. Left: green checkmarks, confident. Right: muted, arrow icons, Stage labels. Bottom callout spans full width. Last line before the demo transition.

**SPEAKER CUE:** End with: "Now let me show you what this looks like." — then cut.

---

## SLIDE 16 — Transition to Demo

---

**HEADLINE (full-slide, centered):**
```
Let's look at it.
```

**BODY:** *(nothing else)*

**LAYOUT:** Mirror Slide 1. Dark background. Headline only. Optionally: blurred or faded preview of the prototype in the background.

**SPEAKER CUE:** Four words. Stop talking. Switch to prototype.

---
---

# Appendix — Slide Spec

## Visual Language

| Element | Value |
|---|---|
| Background | Near-black #0F0F13 or dark navy #0A0F1E |
| Primary text | White #FFFFFF |
| Secondary text | Light grey #94A3B8 |
| Headline size | 40–54pt, Bold |
| Body text | 20–24pt, Regular |
| P1 accent | Electric blue #3B82F6 |
| P2 accent | Amber #F59E0B |
| P3 accent | Orange-red #EF4444 |
| P4 accent | Teal #14B8A6 |
| Selected / positive | Green #22C55E |
| Deferred / muted | 40% opacity, desaturated |
| Rejected | Strikethrough + muted, brief explanation |

## Slide Count by Act

| Act | Slides | Purpose |
|---|---|---|
| ACT 1 — Problems | 1–6 | Establish the four problems, make them felt |
| ACT 2 — Selection | 7–9 | What / Why / So What for Problem 1 |
| ACT 3 — Solutions | 10–15 | Options, pros/cons, chosen combination |
| Close | 16 | Pivot to demo |
| **Total** | **16** | |

## Recommended Tools

- **Figma** — most control over layout, good for dark-theme cards and tables
- **Keynote** — fastest to build, smooth animations, good dark mode
- **Canva** — easy for card layouts, limited on custom typography
- **PowerPoint** — works, but dark themes are more effort

## Animation Guidance

- Slide transitions: **Cross-fade, 0.3s** — nothing faster, nothing bouncier
- Element reveals: **Fade + slight upward drift** — only where content builds (Slides 2, 8, 11)
- Tables: reveal **row by row** when you want to control pacing (Slides 6, 11, 12, 13)
- Never auto-advance — this is a video presentation with narration
