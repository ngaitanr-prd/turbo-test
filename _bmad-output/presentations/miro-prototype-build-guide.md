# Miro Prototype Build Guide
**Source:** `design-artifacts/mockups/screens.html`
**Tool:** Miro Prototypes (add-on — Starter/Business/Enterprise plan required)
**Output:** Clickable, shareable prototype with interactive navigation

---

## How Miro Prototypes works (quick mental model)

Miro Prototypes is built around three concepts:

- **Format container** — wraps all your screens. Gives you Focus mode and Preview mode.
- **Screens** — individual frames inside the Format container. Each screen = one UI state.
- **Connections** — you click any element on a screen, drag the connector icon (⚡) to a target screen. In Preview, clicking that element navigates to the target. There's no in-screen state change — every state needs its own screen.

That last point is critical for how you'll build this. The HTML prototype has interactive states (payment toggle, rule card selection, new rule panel). In Miro Prototypes, **each state = a separate screen**. You link between them with hotspots.

---

## Step 1 — Capture every state as a screenshot

Open `design-artifacts/mockups/screens.html` in Chrome. Set the window to 1280px wide (DevTools → toggle device toolbar → width: 1280, height: 900). For each state below, use Chrome's built-in full-page capture:

> DevTools → Cmd+Shift+P → type "Capture full size screenshot" → Enter

| Screen ID | What to capture | How to trigger it |
|-----------|----------------|-------------------|
| S1 | Order Entry — Insurance (default) | Open the file. This is the default state. |
| S2 | Order Entry — Self-Pay | Click the "💳 Self-Pay" toggle button. |
| S3 | Order Entry — Margin hidden | Click the 👁 eye icon in the Margin column header. |
| S4 | Product Catalog | Click "📦 Product Catalog" in the top nav. |
| S5 | Fee Schedule — Aetna rule selected (Edit) | Click "💰 Fee Schedule". Default state shows edit panel. |
| S6 | Fee Schedule — New Rule form | Click the "+ New Rule" button (top right). |

Save files as: `s1-order-insurance.png`, `s2-order-selfpay.png`, `s3-order-margin-hidden.png`, `s4-catalog.png`, `s5-fee-edit.png`, `s6-fee-new-rule.png`

**You'll have 6 screens total.** That's the exact number needed to cover every clickable interaction in the prototype.

---

## Step 2 — Set up the Miro board

1. Open Miro → create a new board named **"MedOps Prototype — v0.1"**
2. From the left toolbar, open the **Prototypes** panel (puzzle piece icon or "Prototypes" in the app)
3. Click **"+ New prototype"** — this creates a **Format container** on the canvas
4. The Format container is where all your screens live. Rename it: **"MedOps Order Management"**

---

## Step 3 — Create the 6 screens

Inside the Format container, you'll add 6 screens. Do this in order — left to right makes the connector map readable.

**For each screen:**
1. Inside the Format container, click **"+ Add screen"**
2. Set screen size: **1280 × 900** (matches your screenshots)
3. Name the screen (see table below)
4. Import the corresponding PNG: drag the screenshot onto the screen, resize to fill it exactly, then **lock the image** (right-click → Lock) so it doesn't move when you add hotspots

| # | Screen name | PNG file |
|---|-------------|----------|
| S1 | Order Entry — Insurance | s1-order-insurance.png |
| S2 | Order Entry — Self-Pay | s2-order-selfpay.png |
| S3 | Order Entry — Margin Hidden | s3-order-margin-hidden.png |
| S4 | Product Catalog | s4-catalog.png |
| S5 | Fee Schedule — Edit Rule | s5-fee-edit.png |
| S6 | Fee Schedule — New Rule | s6-fee-new-rule.png |

**Set the starting screen:** Right-click S1 → "Set as starting screen". This is where Preview begins.

---

## Step 4 — Map every connection

This is the complete interaction map. Every row is one hotspot: the element you click and where it goes.

### Navigation (top bar tabs) — repeated across all screens

The top bar appears on every screen. You need to add nav hotspots on each screen separately — Miro doesn't have shared components. For efficiency, build the nav hotspots on S1 first, then copy them to S2–S6 and re-link.

| From screen | Hotspot element | Target screen |
|-------------|-----------------|---------------|
| S1 | "📦 Product Catalog" tab | → S4 |
| S1 | "💰 Fee Schedule" tab | → S5 |
| S2 | "📋 New Order" tab | → S1 |
| S2 | "📦 Product Catalog" tab | → S4 |
| S2 | "💰 Fee Schedule" tab | → S5 |
| S3 | "📋 New Order" tab | → S1 |
| S3 | "📦 Product Catalog" tab | → S4 |
| S3 | "💰 Fee Schedule" tab | → S5 |
| S4 | "📋 New Order" tab | → S1 |
| S4 | "💰 Fee Schedule" tab | → S5 |
| S5 | "📋 New Order" tab | → S1 |
| S5 | "📦 Product Catalog" tab | → S4 |
| S6 | "📋 New Order" tab | → S1 |
| S6 | "📦 Product Catalog" tab | → S4 |
| S6 | "💰 Fee Schedule" tab | → S5 |

### Screen-specific interactions

| From screen | Hotspot element | Target screen | What it demonstrates |
|-------------|-----------------|---------------|----------------------|
| S1 | "💳 Self-Pay" toggle button | → S2 | Payment type changes → pricing logic switches |
| S2 | "🏥 Insurance" toggle button | → S1 | Back to insurance flow |
| S1 | 👁 eye icon (Margin column header) | → S3 | Manager hides margin from employees |
| S3 | 🙈 icon (Margin column, hidden state) | → S1 | Restore margin visibility |
| S5 | "+ New Rule" button (top right) | → S6 | Create a new pricing rule |
| S6 | "Cancel" button (in rule editor) | → S5 | Discard new rule, back to edit |
| S6 | "Save New Rule" button | → S5 | Rule saved (returns to edit state) |

### Optional — Submit / Save flows (dead-end screens or loop back)

| From screen | Hotspot element | Target | Notes |
|-------------|-----------------|--------|-------|
| S1 | "Submit Order →" button | → S1 | Loop back — simulates successful submit, same screen |
| S1 | "Save as Draft" button | → S1 | Loop back — draft saved, same screen |
| S4 | "+ Add Product" button | → S4 | Loop back — no add product screen in v0.1 |
| S4 | "⬆ Import from Excel" button | → S4 | Loop back — callout is already on the screen |

---

## Step 5 — Draw the hotspots

For each connection in the table above:

1. On the source screen, draw a **transparent rectangle** over the clickable element
   - Use Miro's Rectangle tool
   - Fill: **0% opacity** (fully transparent)
   - Border: **none** (or a faint blue during build so you can see it, remove before sharing)
   - Size: match the element exactly — cover the full button/tab area

2. With the rectangle selected, drag the **⚡ connector icon** that appears on hover to the target screen

3. The rectangle is now a hotspot. In Preview, clicking anywhere on that rectangle navigates to the target.

**Naming convention for hotspots (helps if you need to edit later):**
- `hs-nav-catalog` → navigates to Product Catalog
- `hs-nav-fee` → navigates to Fee Schedule
- `hs-toggle-selfpay` → payment toggle
- `hs-margin-hide` → eye icon
- `hs-new-rule` → new rule button
- `hs-cancel-rule` → cancel in new rule form

**Hotspot sizing for each interactive element (approximate, at 1280px screen width):**

| Element | Approximate position & size |
|---------|----------------------------|
| "📋 New Order" tab | x:220, y:16, w:110, h:28 |
| "📦 Product Catalog" tab | x:334, y:16, w:130, h:28 |
| "💰 Fee Schedule" tab | x:468, y:16, w:115, h:28 |
| "💳 Self-Pay" toggle | x:172, y:0, w:90, h:34 (inside the toggle container) |
| "🏥 Insurance" toggle | x:0, y:0, w:90, h:34 (inside the toggle container) |
| 👁 eye icon | x:1040, y:8, w:24, h:24 (approx in table header) |
| "+ New Rule" button | x:1140, y:0, w:110, h:36 (top right of fee schedule) |
| "Cancel" button (new rule) | x:930, y:0, w:75, h:32 (inside rule editor) |
| "Save New Rule" button | x:1010, y:0, w:120, h:32 (inside rule editor) |
| "Submit Order →" | x:1090, y:0, w:130, h:36 (form actions area) |
| "Save as Draft" | x:950, y:0, w:120, h:36 (form actions area) |

> Tip: Use DevTools on the HTML file to get exact element positions. Open DevTools → hover over the element → the inspector shows its bounding box coordinates.

---

## Step 6 — Hide connectors for a clean view

With 20+ connections, the canvas gets visually noisy. Before entering Focus or Preview:

1. Select the Format container
2. Click the **three-dot menu (⋯)**
3. Select **"Hide connectors"**

You can re-show them anytime for editing. In Focus mode there's a dedicated **Hide | Show connectors** toggle in the top-left.

---

## Step 7 — Preview and share

### Test it yourself first

1. Inside the Format container, click **"Preview"** (play button icon)
2. You'll enter full-screen Preview mode
3. Click through every interaction using the connection map above — verify each hotspot lands on the right screen
4. Press **Escape** to exit Preview

### Share with Alex

1. Click **"Share"** on the Miro board
2. Set link access to **"Anyone with the link can view"**
3. Enable **"Open in Focus mode"** — this is critical. External viewers only see the prototype in Focus mode, not the full canvas. They'll click through it exactly like a real app.

Alternatively: inside the Format container, click **"Share prototype"** → copy the direct prototype link. This opens directly in Focus mode with no board context visible.

---

## Flow diagram — what Alex will click through

```
START
  │
  ▼
S1: Order Entry — Insurance
  │   [tab] Product Catalog ──────────────────────────► S4: Product Catalog
  │   [tab] Fee Schedule ──────────────────────────────► S5: Fee Schedule (Edit)
  │   [toggle] Self-Pay ───────────────────────────────► S2: Order Entry — Self-Pay
  │   [view eye] ────────────────────────────────────────► S3: Order Entry — Margin Hidden
  │   [Submit / Save Draft] ───────────────────────────► S1 (loop)
  │
  ▼
S2: Order Entry — Self-Pay
  │   [tab] New Order ─────────────────────────────────► S1
  │   [tab] Product Catalog ───────────────────────────► S4
  │   [tab] Fee Schedule ──────────────────────────────► S5
  │   [toggle] Insurance ──────────────────────────────► S1
  │
  ▼
S3: Order Entry — Margin Hidden
  │   [hide icon] ────────────────────────────────────────► S1 (restore)
  │   [tabs] ──────────────────────────────────────────► S4 / S5
  │
  ▼
S4: Product Catalog
  │   [tab] New Order ─────────────────────────────────► S1
  │   [tab] Fee Schedule ──────────────────────────────► S5
  │
  ▼
S5: Fee Schedule — Edit Rule (Aetna selected)
  │   [tab] New Order ─────────────────────────────────► S1
  │   [tab] Product Catalog ───────────────────────────► S4
  │   [+ New Rule] ────────────────────────────────────► S6
  │
  ▼
S6: Fee Schedule — New Rule Form
      [Cancel] ────────────────────────────────────────► S5
      [Save New Rule] ─────────────────────────────────► S5
      [tabs] ──────────────────────────────────────────► S1 / S4
```

---

## Demo script — what to click during recording

| Segment | Screen | Click sequence | What it shows |
|---------|--------|---------------|---------------|
| 1. Order entry flow | S1 | Narrate the form top to bottom. Point to auto-filled fields (HCPCS, price, cost, margin). Point to the summary bar. | Pricing populates automatically — no manual lookup. |
| 2. Payment toggle | S1 → S2 | Click "💳 Self-Pay" | Switching payment type changes the pricing logic. |
| 3. Back to insurance | S2 → S1 | Click "🏥 Insurance" | Seamless toggle. |
| 4. Margin visibility | S1 → S3 | Click 👁 eye icon | Manager can hide margin from employee view. |
| 5. Product Catalog | S1 → S4 | Click "📦 Product Catalog" tab | Show the searchable catalog, approval flag on row 4, Import from Excel callout. |
| 6. Fee Schedule | S4 → S5 | Click "💰 Fee Schedule" tab | Show Aetna rule selected. Point to "Base × 1.15" formula. Show resolved rates table — "23 products, one rule." |
| 7. New rule | S5 → S6 | Click "+ New Rule" | Show the empty rule form. Narrate: "Adding a new payer is a new rule, not 800 rows." |
| 8. Back to edit | S6 → S5 | Click "Cancel" | Wrap up — return to steady state. |

---

## Build time estimate

| Task | Time |
|------|------|
| Screenshot all 6 states | 10 min |
| Set up Format container + 6 screens | 15 min |
| Import and lock all screenshots | 10 min |
| Draw all hotspot rectangles | 30 min |
| Connect all hotspots | 20 min |
| Test in Preview mode | 10 min |
| **Total** | **~1.5 hours** |
