# BB First Sale Calculator

Internal Krowne pricing tool for first-sale valuation on BB-sourced equipment. Single-file, dependency-free HTML app — published via GitHub Pages from `index.html`.

**Live page:** enable GitHub Pages (Settings → Pages → Deploy from branch → `main` / root) and the tool serves at `https://<owner>.github.io/bb-first-sale-calc/`

## What it does

Takes the Krowne cost of equipment from BB, the factory cost, a mark-up tier, tariff %, brokerage fees, and freight, and builds up the **Selling Price to Dealer**. It then shows two comparisons side by side:

| Section | Purpose |
|---|---|
| **Selling Price Build-Up** | Line-item build from BB cost → mark-up → tariff → brokerage → freight → Selling Price to Dealer |
| **Price Comparison** | Dealer Net tier (5% or 10%, per dropdown) vs. Budgetary Price to End User / Consultant (always 20%), plus $ and % difference |
| **Pass-Thru Tariff Reduction** | Tariff on factory cost vs. tariff on BB direct cost — the first-sale savings |
| **BB Direct to Customer** | What the customer would pay buying direct from BB, and how that compares to the 20% Budgetary Price |

## Calculation logic

- **Krowne Mark-Up** applies to *Krowne Cost of Equipment from BB* only.
- **Estimated Tariff** is calculated against *Factory Cost of Equipment* (the factory→BB sale price) — this is the first-sale mechanic, not the Krowne cost.
- **Estimated Freight** auto-calculates at 12.5% of the Krowne cost from BB, and can be manually overridden.
- **Brokerage and Misc. Fees** default to $200 flat and are added directly into the selling price.
- **HTS Code** is locked at `9403.20.00.90` for this equipment category.
- Fields in the BB Direct section mirror the inputs above by default; typing in any of them breaks the link so it holds a manual value.

Mark-up guide: **5% or 10%** for Dealer Net Pricing · **20%** for Consultant or End User Budgetary Pricing.

## Known behavior (not a bug)

The **Budgetary Price vs. Direct Cost Difference** box does not change when switching the Krowne Mark-Up dropdown between 5% and 10%. By design, that card always compares the fixed 20% Budgetary Price against the BB Direct Cost — neither value depends on the dropdown.

If it should instead track the selected mark-up, the change is one line in `calc()`: use `sellingPrice` in place of `enduserPrice` in the `bbVsEnduserDiff` calculation, plus a label update on that card. A version of this was explored and intentionally reverted.

## Outputs

- **Export Entire Document as PDF** — full page, print-styled (white header, read-only inputs, page metadata line)
- **Export Selling Price Build-Up as PDF** — build-up card and quote reference only
- **Email Selling Price Summary** — opens a `mailto:` draft with the build-up as plain text

Both exports stamp in the Prepared For / Quote Reference, Krowne Salesperson, Sales Order #, and date.

## Editing

Everything — markup, CSS, and JS — lives in `index.html`. No build step, no dependencies. Open it in a browser to test, commit, and Pages redeploys.

Brand tokens are CSS variables at the top of the `<style>` block (`--krowne-teal: #01A79D`, `--krowne-black: #282828`).

---

Krowne Metal Specialties · 100 Haul Rd., Wayne, NJ 07470 · quotes@krowne.com
