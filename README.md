# Freight Load Selection & Profitability Model

A weighted multi-criteria decision model for accepting or declining freight.

Built on eighteen completed loads from my own operation. Cost-per-mile inputs are derived from my own settlement history, using multi-year averages for the fixed and variable components and the most recent three weeks as current-period figures. These are actual operating numbers from a single owner-operator. They are not third-party audited results and, except for the explicitly labeled tire reserve, they are not industry benchmarks.

**What it is:** an owner-operator decides in minutes whether to take a load, using one visible number — the rate. This model makes the rest of the decision explicit: true cost per mile, deadhead, hours committed, reload strength at the destination, and four other dimensions that never appear on a rate confirmation.

**Why it's here:** the interesting part is not the spreadsheet. It's what happened when I checked it — against eighteen loads I had already rated, and by reconciling the cost stack to my own settlement history. Those checks found errors in my own work. Both are documented below rather than quietly fixed.

---

## Headline numbers

| | |
|---|---|
| Trips analysed | 18 |
| Miles | 19,214 |
| Revenue | $41,501.02 |
| Blended rate | $2.16 / mile gross, $1.28 / mile net of all-in cost |
| Deadhead | 12.7% |
| Cost stack source | owner-operator settlement history, using multi-year averages and the most recent three weeks as current-period figures |

---

## Three findings worth reading

### 1. A cost the model was charging that did not exist

Version 1 carried a $0.280 per mile truck payment. The equipment is owned outright.

Break-even moved from $1.342 to $0.934 across the rebuild, and it is worth being precise about why, because that whole move is often attributed to one line:

| Change | Effect | Running total |
|---|---|---|
| Version 1 all-in cost per mile | — | $1.342 |
| Truck payment removed | −$0.280 | $1.062 |
| Fuel re-priced to actual, net of discount | −$0.010 | $1.052 |
| Maintenance reserve cut $0.180 → $0.120 | −$0.060 | $0.992 |
| Tolls/securement replaced by DEF, fuel tax, misc | +$0.020 | $1.012 |
| Fixed cost re-derived from statement lines | −$0.079 | **$0.934** |

The truck payment is $0.280 of a $0.408 move — about 69%. The rest came from reconciliation and revised assumptions.

Against a comparable operator carrying a $33,600 annual note, owning the equipment outright is $0.2937 per mile of structural advantage: $5,643 across this sample.

### 2. Estimating a cost stack and never checking it

Version 2's costs came from industry reserve figures. Reconciling to an operating statement found four errors:

| Line | Estimated | Actual | |
|---|---|---|---|
| Maintenance & repair | $0.180 | $0.065 | 2.8× over-reserved |
| Diesel | $3.70/gal | $4.93/gal | off by $1.23 |
| Annual miles | 120,000 | derived 114,400 | no basis for the original |
| Tires | $0.045 | not on the statement at all | see below |

The errors ran in opposite directions and mostly cancelled. The version 2 total was accurate to within eight cents **for entirely the wrong reasons**.

**The tire line I got wrong twice.** The statement shows a tire fund accrual and a fund disbursement offsetting to the cent, and I first read that as evidence tires cost nothing. Prime runs a tire fund for lease drivers, not owner-operators — for my unit those lines are vestigial. Tires are bought personally and never touch a settlement. The statement doesn't show a zero cost; it shows *no* cost, which is different. The model carries $0.045/mile as a reserve, flagged as the one line with no source document behind it.

### 3. The result I did not want

**First, what this test is and is not.** All 18 loads were accepted, and I rated each one after delivery. This compares model output against *retrospective quality ratings*. It is not a test against accept-or-decline decisions, and nothing here shows whether the model would catch a load worth refusing.

Correlation between model score and my rating is **0.56**. Net dollars per mile taken alone is **0.62**.

A single arithmetic column tracks my ratings better than the eight-dimension model built on top of it. Re-tuning weights against eighteen rows would improve that number and destroy its meaning, so the weights stayed where reasoning put them.

Two of the lowest four overlap between model and rating; two of the highest four do. The decline side has never been exercised, so no claim is made about it.

---

## How the model ties to the statement

Two figures, because they answer two questions:

| | Model | Statement | Gap |
|---|---|---|---|
| Like-for-like — model set to statement values | $0.832 | $0.838 | $0.006 |
| As configured — what I actually run | $0.917 | $0.838 | $0.085 |

The first is the arithmetic check and it passes. The second is $0.085 higher by deliberate, itemized choice: maintenance reserved $0.055 above actual, a $0.045 tire reserve the statement doesn't carry, and $0.015 back from normalizing annual miles. Quoting the $0.006 alone would imply the model matches the statement. It doesn't, and it shouldn't.

---

## Method

**Three calculated dimensions** — net rate per total mile, net dollars per hour committed, deadhead percentage.

**Five judgment dimensions** — destination value, dwell risk, securement burden, route conditions, hours-of-service feasibility. Scored 1–5 at the moment of the offer, because reload strength and facility behaviour are field knowledge that appears on no rate sheet.

**Three hard gates** that override the weighted score entirely: negative net contribution, deadhead above tolerance, and legal infeasibility or a blacklisted facility. A weighted average can be dragged upward by strong dimensions while the load remains unacceptable.

---

## Files

| File | What it is |
|---|---|
| `load-selection-case-study.pdf` | The full write-up. Start here. |
| `load-selection-model.xlsx` | Working model, 7 tabs, 423 formulas, fully recalculating |
| `load-selection-case-study.docx` | Editable source |

Workbook tabs: **README** · **Assumptions** · **Load Board** · **Scoring Rules** · **Settlement Recon** · **Score a Load** · **Testing**

---

## Limitations

- **No decline data at all.** All 18 loads were accepted. Nothing here speaks to whether the model would catch a bad load before the fact.
- **Ratings are retrospective**, assigned after delivery, so outcome leaks into them.
- **One load of eighteen is reconciled** to a settlement. That trip differed by 5.3% on total miles and $35.40 on revenue. One observation is not a pattern and no correction was applied to the rest on the strength of it.
- **The tire reserve has no source document.** $0.045/mile is an industry figure — the weakest number in the stack.
- **Band thresholds were cut from the same 18 observations** used to report the correlation, making it in-sample and optimistic.
- **The statement covers one tractor**, January 2022 onward. Roughly three and a half earlier years of owner-operator history aren't recoverable, and that truck was run considerably harder.

Customer and facility names are anonymized. Lane geography, mileage, and revenue are unaltered.

---

## Why a freight model is in a business analysis portfolio

The freight context is incidental. The transferable pattern: establish true unit cost, weight the criteria that drive the outcome, keep calculated separate from judged, put hard gates around failures no weighted average should approve — then check it against whatever record of past outcomes exists and publish what the check said.

Anyone can build a cost model from published benchmarks. Reconciling one to a real source document from the operation, finding four material errors in your own work, and rewriting rather than defending is the part that transfers.

---

**Christopher D. Sheppard** — Marine Corps veteran, owner-operator, Microsoft PL-900.
Moving from regulated field operations into business analysis, automation, and applied AI.

[LinkedIn](https://linkedin.com/in/christopherdsheppard)
