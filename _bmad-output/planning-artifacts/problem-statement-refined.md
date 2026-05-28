# Problem Statement — Refined
**Project:** turbo-test
**Date:** 2026-05-27
**Informed by:** problem-space-analysis.md, problem-statement.md, brainstorming session, problem validation conversation

---

## The Four Distinct Problems Alex Has

Everything Alex described in the initial conversation collapses into four genuinely distinct problems. Each has a different root and requires a different type of fix. They are sequenced — not arbitrary.

---

### Problem 1 — No Reliable Master Data *(attacking now)*

Product costs, fee schedules, pricing rules, and payer rates live in hidden Excel tables and people's memory. There is no single place to look something up and trust the answer.

**Consequence:** The same order processed by two people produces two different prices, different margins, and different patient balances. Any automation built on top of this data inherits every mistake already in it.

**Type:** Data problem — the structured information doesn't exist reliably.
**Fix:** Build a canonical product catalog and rules-based fee schedule.

---

### Problem 2 — People Are the Middleware *(Stage 2)*

After an order is captured, the team re-enters it manually into vendor portals, assembles PDFs by hand, and routes by email. Every system is disconnected, and a person bridges each gap.

**Consequence:** Throughput hits a ceiling. Scaling the business requires proportional headcount growth to perform the same manual steps.

**Type:** Integration problem — systems don't talk to each other.
**Fix:** Automate handoffs between the order system and vendor portals, document generation, and routing logic.

---

### Problem 3 — Compliance Controls Are Outside the Workflow *(Stage 3)*

The HCPCS approval gate exists in SharePoint. Prior authorization requirements are tracked in experienced employees' heads. Neither is enforced inside the order flow.

**Consequence:** Approvals can be skipped. Prior auth gets missed. Claim denials, audit exposure, and no paper trail.

**Type:** Governance problem — controls exist but aren't embedded in the workflow.
**Fix:** Embed approval gates and prior auth checks directly into the order flow, with an audit trail.

---

### Problem 4 — Critical Knowledge Exists Only in People's Heads *(Stage 4)*

Vendor routing logic, prior auth rules, product exceptions, and pricing edge cases are not written down anywhere the system can use. When someone leaves, the knowledge leaves with them.

**Consequence:** Onboarding takes months. Decisions are inconsistent. The business is a key-person risk.

**Type:** Knowledge problem — rules exist but aren't encoded anywhere.
**Fix:** Progressively encode undocumented rules into the system as each stage is built.

---

## Why These Four Are Genuinely Distinct

The overlap most likely to create confusion: Problems 3 and 4 both involve things "not being written down." The distinction is precise:

- **Problem 3** — The rule *is* known and documented (the approval gate exists in SharePoint). It just isn't enforced *inside* the workflow. The fix is enforcement, not documentation.
- **Problem 4** — The rule isn't documented *anywhere*. Prior auth requirements and vendor routing logic exist only in people's heads. The fix is codification before enforcement is even possible.

| Problem | What's missing | How you fix it |
|---|---|---|
| 1 — Data | Structured information doesn't exist reliably | Build a canonical catalog and rules engine |
| 2 — Integration | Systems don't talk — people bridge the gaps | Automate handoffs between systems |
| 3 — Governance | Controls exist but aren't enforced in the flow | Embed approval gates and prior auth checks |
| 4 — Knowledge | Rules exist but aren't written anywhere | Encode rules the system can read and enforce |

---

## Verdict: The Current Solution Attacks One Problem

**The solution being built:** Product Catalog + Fee Schedule (rule-based) + Order Entry Form.

**The one problem it attacks:** *"The master data is not reliable, and that unreliability flows directly into every order."*

### Why all three components trace back to the same root

| Component | How it connects to Problem 1 |
|---|---|
| Product Catalog | Is the master data fix — products, HCPCS codes, costs, and MSRP now live in one canonical place |
| Fee Schedule (rule-based) | Is the master data fix — pricing rules are no longer embedded in Excel formulas or people's heads |
| Order Entry Form | Is the enforcement mechanism — it makes employees consume the reliable data instead of the old Excel |

### Why the Form is not a separate problem

The Form is tempting to read as a separate UX or workflow problem. It isn't. Without the Form, the canonical data exists but employees can still bypass it and reference old Excel sources. The Form is what closes the behavioral loop — it makes the data fix operational, not just structural.

The test: remove any one component and the problem remains open.
- No Catalog → order entry still references scattered product data
- No Fee Schedule → pricing logic still lives in Excel or people's heads
- No Form → canonical data exists but nothing enforces its use

All three are necessary. All three respond to the same root.

### What this solution explicitly does not solve

Problems 2, 3, and 4 are real and documented. They are deferred — not forgotten. They are sequenced after Problem 1 because automating on top of unreliable data would propagate errors faster, not eliminate them.

