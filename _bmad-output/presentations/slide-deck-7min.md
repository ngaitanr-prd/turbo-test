# Slide Deck — 7 Minutes · 7 Frames
**Tool:** Miro · **Format:** Video presentation
**Audience:** Alex (stakeholder)
**Arc:** Problems → Selection → Solutions → Demo

---

## Timing Map

| Frame | Title | Time |
|---|---|---|
| 1 | Hook | 0:10 |
| 2 | The Four Problems | 1:15 |
| 3 | Why We're Starting Here | 1:15 |
| 4 | Order Entry — Three Options | 1:00 |
| 5 | Catalog + Fee Schedule | 1:00 |
| 6 | The Chosen Solution | 0:45 |
| 7 | Demo Handoff | 0:10 |
| | **Breathing room** | ~1:25 |
| | **Total** | **~7:00** |

---
---

## FRAME 1 — Hook
**Time on screen: 10 seconds**

---

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│                                                             │
│         Before we build anything —                         │
│         let's name what's actually broken.                  │
│                                                             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**On slide:** Headline only. Nothing else.

**Miro note:** Dark frame background (#0F0F13). White text, large. Full frame — no margin content.

---

## FRAME 2 — The Four Problems
**Time on screen: ~1:15**

---

```
┌─────────────────────────────────────────────────────────────┐
│  Alex's operation has four problems. Each has a different   │
│  root — and they're sequenced.                              │
├───────────────────────────┬─────────────────────────────────┤
│  P1 — No Reliable         │  P2 — People Are                │
│  Master Data              │  the Middleware                 │
│  ─────────────────────    │  ───────────────────────────    │
│  Pricing, fee schedules,  │  After capture, the team        │
│  and payer rates live in  │  re-enters every order into     │
│  hidden Excel tables and  │  vendor portals by hand,        │
│  people's heads.          │  assembles PDFs, routes         │
│                           │  by email.                      │
│  → Two employees process  │                                 │
│  the same order → two     │  → Growth requires more staff   │
│  different prices.        │  doing the same manual steps.   │
│                           │                                 │
│  ★ Attacking this now     │  Stage 2                        │
├───────────────────────────┼─────────────────────────────────┤
│  P3 — Compliance          │  P4 — Critical Knowledge        │
│  Controls Outside         │  in People's Heads              │
│  the Workflow             │                                 │
│  ─────────────────────    │  ───────────────────────────    │
│  The HCPCS approval       │  Vendor routing logic, prior    │
│  gate lives in            │  auth rules, pricing            │
│  SharePoint — outside     │  exceptions — none of it        │
│  the order flow.          │  is written anywhere the        │
│                           │  system can read.               │
│  → Approvals get skipped. │                                 │
│  No audit trail.          │  → When someone leaves,         │
│                           │  the knowledge leaves.          │
│  Stage 3                  │  Stage 4                        │
└───────────────────────────┴─────────────────────────────────┘
```

**On slide:**
- 2×2 grid of problem cards
- Each card: name (bold) + 2-sentence description + 1-line consequence (→ format)
- P1 card: distinct highlight — colored border or background tint. Label: **★ Attacking this now**
- P2, P3, P4: muted. Small "Stage X" label bottom-right of each card.

**Miro note:** Use Miro cards or sticky notes in a 2×2 grid. P1 card: blue border (#3B82F6). Others: grey border, lower opacity text.

---

## FRAME 3 — Why We're Starting Here
**Time on screen: ~1:15**

---

```
┌─────────────────────────────────────────────────────────────┐
│  WHAT      No single source of product and pricing data.    │
│            It lives in Excel tables, formulas, and          │
│            people's memory. Same order, different people    │
│            → different prices, different margins.           │
├─────────────────────────────────────────────────────────────┤
│  WHY       It's not a priority. It's a prerequisite.        │
│  FIRST                                                      │
│            ┌─────────────────────┐                          │
│            │ P1: No Master Data  │ ← fixing this            │
│            └──────────┬──────────┘                          │
│                       │ unlocks                             │
│            ┌──────────┼──────────┬──────────┐              │
│            ▼          ▼          ▼          ▼              │
│         Automate   Auto-fill  Track      Enforce           │
│         vendor     pricing    prior      approval           │
│         routing    in forms   auth       gates              │
│                                                             │
│   Automating on top of bad data propagates errors faster.   │
├─────────────────────────────────────────────────────────────┤
│  SO WHAT   Every feature we build in Stages 2–4 has a       │
│            trustworthy foundation instead of inheriting     │
│            the same broken data.                            │
└─────────────────────────────────────────────────────────────┘
```

**On slide:**
- Three horizontal bands: WHAT / WHY FIRST / SO WHAT
- Each band gets a label (left, bold, accent color) and content (right)
- WHY FIRST band contains the dependency tree — this is the visual hero
- SO WHAT band is short and confident — one sentence

**Miro note:** Three horizontal sections separated by thin lines. Dependency tree in the WHY band — use Miro connectors. The four unlocked nodes should feel "downstream" visually (dimmer, smaller, below P1).

---

## FRAME 4 — Order Entry: Three Options
**Time on screen: ~1:00**

---

```
┌─────────────────────────────────────────────────────────────┐
│  ORDER ENTRY — Three fundamentally different approaches.    │
├───────────────────┬───────────────────┬─────────────────────┤
│  Option A         │  Option B         │  Option C           │
│  Web App          │  AI-Assisted      │  Clinic-Side Intake │
│                   │  Entry            │                     │
│  Employee opens   │  AI reads clinic  │  Clinic fills a     │
│  a form, picks    │  docs (fax, PDF), │  form directly in   │
│  from a catalog   │  extracts data,   │  Alex's portal.     │
│  dropdown.        │  pre-fills form.  │  Order arrives      │
│  Pricing auto-    │  Employee reviews │  pre-priced.        │
│  populates.       │  and corrects.    │                     │
│                   │                   │                     │
│  ✅ No tech risk  │  ✅ Less typing   │  ✅ Least internal  │
│  ✅ Full control  │  ✅ Platform-     │  effort             │
│  ✅ Foundation    │  agnostic         │                     │
│  for Stage 2–4   │                   │                     │
│                   │  ❌ AI accuracy   │  ❌ External        │
│                   │  drops on faxed/  │  dependency Alex    │
│                   │  handwritten docs │  can't control      │
│                   │  ❌ Wrong HCPCS   │  ❌ Two-tier        │
│                   │  → billing error  │  problem if some    │
│                   │  ❌ Solves a pain │  clinics don't      │
│                   │  Alex didn't raise│  adopt              │
├───────────────────┼───────────────────┼─────────────────────┤
│  ✅ SELECTED      │  → Stage 2        │  Revisit later      │
└───────────────────┴───────────────────┴─────────────────────┘
```

**On slide:**
- Three equal columns, each an option
- Header row: option name (bold)
- Middle rows: how it works + pros (✅) + cons (❌)
- Bottom row: verdict — Option A gets green "SELECTED" badge, others get muted labels

**Miro note:** Three Miro cards or table columns. Option A: green bottom border or badge. Options B and C: grey, slightly muted. Don't gray them out completely — they're real candidates for later stages.

---

## FRAME 5 — Catalog + Fee Schedule
**Time on screen: ~1:00**

---

```
┌─────────────────────────────────────────────────────────────┐
│  Two more dimensions. One key insight each.                 │
├──────────────────────────┬──────────────────────────────────┤
│  CATALOG MANAGEMENT      │  FEE SCHEDULE                    │
│                          │                                  │
│  The cold-start problem. │  Rows don't scale. Rules do.     │
├─────────────┬────────────┼────────────┬────────┬────────────┤
│  Manual     │  Mining    │ Traditional│ Rule-  │ ERA/EOB-   │
│  Entry      │  from      │ Lookup     │ Based  │ Driven     │
│             │  Excel     │            │ Engine │            │
│             │            │            │        │            │
│  Admin      │  System    │ One row    │ Admin  │ System     │
│  builds     │  reads     │ per payer  │ defines│ learns     │
│  catalog    │  Alex's    │ × HCPCS    │ rules. │ rates from │
│  from       │  Excel     │ × ZIP ×    │ System │ actual     │
│  scratch.   │  history   │ rate.      │ computes│ insurance │
│             │  on setup. │            │ rates. │ remittances│
│             │  Admin     │            │        │ (ERA/EOB). │
│             │  reviews,  │            │        │ Self-      │
│             │  not       │            │        │ corrects   │
│             │  builds.   │            │        │ over time. │
│             │            │            │        │            │
│  ❌ Months  │  ✅ Day-   │ Year 1: 50 │ Year 1:│ ✅ Zero    │
│  of setup   │  one       │ Year 2: 200│ 5 rules│ manual     │
│  before     │  accuracy  │ Year 3: 800│ Year 2:│ maintenance│
│  useful     │  ✅ Actual │ rows ↑ fast│ 8 rules│            │
│             │  orders,   │            │ Year 3:│ ❌ Needs   │
│             │  not theory│ ❌ One rate│12 rules│ payment    │
│             │            │ change =   │ ↑ stays│ history to │
│             │            │ update     │ manage-│ bootstrap  │
│             │            │ every row  │ able   │ ❌ Requires│
│             │            │ it hits    │        │ remittance │
│             │            │            │        │ processing │
│             │            │            │        │ infra      │
├─────────────┼────────────┼────────────┼────────┼────────────┤
│             │ ✅ SELECTED│            │✅ SELEC│ → Stage 3+ │
└─────────────┴────────────┴────────────┴────────┴────────────┘
```

**On slide:**
- Two sections (Catalog / Fee Schedule) divided vertically
- Catalog section has two option columns; Fee Schedule has three
- The scaling row counts (Year 1/2/3) are the visual hero of the fee schedule section
- ERA/EOB-driven shown as a deferred candidate — muted styling, "→ Stage 3+" label
- Selected options get green badges, rejected get muted styling

**Miro note:** One Miro frame split into two halves with a divider line. Left half = 2 catalog columns, right half = 3 fee schedule columns. The Year 1/2/3 row count comparison should be visually stark — make the numbers big enough to read at a glance. ERA/EOB column: grey border, lower opacity text, same treatment as deferred options in Frame 4.

---

## FRAME 6 — The Chosen Solution
**Time on screen: ~0:45**

---

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   Web App  +  Mining  +  Rule-based fee schedule           │
│                                                             │
│   ─────────────────────────────────────────────────────    │
│                                                             │
│   "Build minimum scope on maximum foundation."              │
│                                                             │
│   ─────────────────────────────────────────────────────    │
│                                                             │
│   Every decision we're making today is still the           │
│   right decision in Stage 4.                                │
│                                                             │
│   • Web interface → Stage 2–4 features have a home         │
│   • API layer → AI entry + clinic portal plug in later      │
│   • Rules engine → new payer = new rule, not a migration   │
│   • Mining → data is accurate from day one                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**On slide:**
- Top: the three-component combination in large bold text
- Divider line
- Design principle as a pull quote — the biggest text on the slide after the combination
- Divider line
- Four bullets below (smaller, supporting)

**Miro note:** The design principle ("Build minimum scope on maximum foundation.") should be the visual anchor — center it, make it large, give it a contrasting color or a box. The four bullets below are supporting detail, not the message.

---

## FRAME 7 — Demo Handoff
**Time on screen: 10 seconds**

---

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│                                                             │
│                     Let's look at it.                      │
│                                                             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**On slide:** Headline only. Mirrors Frame 1.

**Miro note:** Same dark background as Frame 1. Optionally: faint blurred preview of the prototype behind the text. Switch to prototype immediately after.

---
---

# Miro Build Notes

## Frame settings
- All frames: 1920×1080px (16:9) — matches video output
- Background: #0F0F13 (near-black) — set at frame level, not canvas
- Use Miro's **Presentation Mode** to advance frames in sequence during recording

## Card / element colors

| Element | Color |
|---|---|
| P1 card border | #3B82F6 (blue) |
| P2–P4 card border | #374151 (muted grey) |
| Stage X labels | #6B7280 (grey) |
| ✅ SELECTED badge | #22C55E (green) |
| → Deferred label | #6B7280 (grey) |
| Design principle text | #FACC15 (amber/gold) — makes it pop on dark |
| Primary text | #F9FAFB |
| Secondary text | #9CA3AF |

## Typography (Miro text elements)
- Frame headlines: 36–44pt, Bold
- Card headlines: 24pt, Bold
- Body text: 16–18pt, Regular
- Labels (Stage X, verdict): 13pt, Medium or Italic

## What to build first
1. Frame 2 (The Four Problems) — most complex layout, set the visual language here
2. Frame 4 (Order Entry) — three-column comparison, reuse the column structure for Frame 5
3. Frame 5 (Catalog + Fee Schedule) — adapt Frame 4 columns
4. Frames 1, 7 — 5 minutes each, do these last
5. Frames 3, 6 — straightforward once the visual language is set
