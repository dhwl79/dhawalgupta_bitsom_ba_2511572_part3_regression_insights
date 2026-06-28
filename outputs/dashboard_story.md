# Dashboard Story: Executive Sales & Profitability Review

*Prepared for: Retail Leadership Team*
*Covering: Jan 2024 – Dec 2025, 4,200 orders, ₹21.70 Cr in sales*

## Executive Summary

The business grew sales 4.3% year-over-year, but profit only grew 2.2% — we're getting
slightly less profitable as we get bigger. Pulling every view on the dashboard together
tells one connected story: **almost every margin and risk signal in the data points to the
same place — Furniture.** It has the weakest margins in the catalog, carries the heaviest
discounts, and gets returned more than twice as often as our other two categories. None of
our four regions, three customer segments, or four shipping modes show a problem anywhere
close to that scale. This isn't a portfolio of small issues — it's one connected,
fixable problem sitting inside an otherwise healthy business.

## What Is Performing Well

Technology is the clear engine of this business: 18%+ margins across all four of its
sub-categories, the lowest average discount levels in the catalog, and the lowest return
rates (2.7–3.5%). It's profitable, it's not being discounted away, and customers keep it.
Regionally, there's nothing to fix — South, North, East, and West all sit within 0.4
percentage points of each other on margin, which means execution is consistent
geographically and the team doesn't need to spend energy on a regional turnaround. Same
Day shipping, while a small share of volume, has both the fastest delivery and the lowest
return rate of any mode, and customer ratings are stable (~4.0–4.1 out of 5) regardless of
how fast an order arrives — service quality is not degrading anywhere we can see.

## What Is Underperforming

Furniture is the one category where every signal is weak at once: Bookcases and Tables
run 5.7% margin, Chairs 8.2%, Furnishings 7.9% — roughly a third of Technology's margin on
the same sales effort. It's also the most heavily discounted category and, not
coincidentally, the most returned: Bookcases, Furnishings, Chairs, and Tables fill four of
the catalog's five highest return-rate spots. Separately, First Class shipping — despite
being reasonably fast — has the highest return rate of any shipping mode (5.1%), which
breaks the assumption that "faster shipping means happier customers." And profit growth
trailing sales growth (2.2% vs. 4.3%) is itself a quiet underperformance signal sitting on
top of every other chart on this dashboard.

## Risks Visible on the Dashboard

The connected risk is Furniture: weak margin, heavy discounting, and high returns
reinforcing each other. If Furniture volume keeps growing at its current mix, it will keep
dragging down company-wide margin the way it's already contributing to the sales-vs-profit
gap in the trend chart. A second, smaller risk: Home Office customers return products
~42–45% more often than Consumer or Corporate, even though they buy just as much and rate
their experience just as highly — a cost that doesn't show up until you specifically look
for it. Across the whole catalog, the discount-to-margin relationship (r = ‑0.60) means any
discount push beyond ~30% is, on average, **selling at a loss**, which is a policy risk if
discount approval isn't currently capped.

## Opportunities Visible on the Dashboard

Technology has earned the right to more investment: every dimension on this dashboard
— margin, discount discipline, return rate — favors it over the other two categories, and
it's already the largest profit contributor. South region's combination of the highest
sales *and* the highest margin of any region suggests there's a regional practice worth
documenting and sharing with the other three regions. And because the South region filter
action shows the Furniture problem persists even within South's otherwise-strong numbers,
we know the fix is genuinely category-level — not a regional execution gap — which makes
it a cleaner, more scoped project to staff.

## Recommended Business Actions

1. **Open a focused Furniture initiative** covering pricing, discount caps, and a returns
   root-cause review together — not three separate workstreams — since the dashboard shows
   these three problems are the same problem.
2. **Cap discount approval** (e.g., manager sign-off above ~25%, hard floor around 30–35%)
   given the order-level data showing margin turns negative in that range.
3. **Shift incremental marketing/inventory budget toward Technology**, where every
   indicator supports more investment rather than less.
4. **Investigate First Class returns and Home Office returns** as two specific, scoped
   follow-up questions — both are real but smaller signals than Furniture.
5. **Set next year's target on profit growth, not just sales growth**, so category mix
   shifts (like more Furniture volume) don't quietly erode margin again.

## Limitations of This Dashboard

This dashboard shows *what* is happening, not definitively *why* — for example, it cannot
tell us whether Furniture returns are caused by damage in transit, product quality, or
mismatched customer expectations; that requires a sample review of actual return reasons,
which weren't in this dataset. The data covers two years for one company, so seasonal
effects and year-to-year noise are hard to fully separate from real trend. A few records
have missing `customer_rating` (32) or `campaign_channel` (24) values, and the source data
maps "Rajasthan" to two different regions (North and West) — neither materially changes
the conclusions above, but both are worth cleaning up at the source for future reporting
(see README, Section: Assumptions and Limitations).

## Suggested Next Analysis

1. Pull a sample of Furniture return reason codes (if collected) to find the specific root
   cause rather than just the pattern.
2. Run a controlled discount-cap test in Furniture only, and measure the margin/volume
   trade-off before rolling any policy out company-wide.
3. Segment First Class shipping by order characteristics (product type, order value,
   customer segment) to isolate why its return rate is highest despite being fast.
4. Re-run this same dashboard next quarter to check whether the sales-vs-profit growth gap
   (#1) is closing, holding steady, or widening — that single trend is the best early
   warning signal for whether today's recommendations are working.
