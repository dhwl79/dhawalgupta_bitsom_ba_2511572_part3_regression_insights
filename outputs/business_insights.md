# Business Insights

Each insight below follows the same structure: what the dashboard shows, the data behind
it, what it means for the business, and a recommended next step. Figures are drawn
directly from `dashboard_sales_data.xlsx` (4,200 orders, Jan 2024 – Dec 2025) and match the
calculations in `tableau/executive_dashboard.twbx`.

---

### 1. Sales Trend — Growth is real but slowing relative to profit

**Observation:** Total sales grew year-over-year, but profit grew more slowly, so the
business is getting *less profitable per rupee of sales growth* over time.

**Data evidence:** Sales rose from ₹10.62 Cr (2024) to ₹11.08 Cr (2025), +4.3% YoY. Profit
rose from ₹1.647 Cr to ₹1.683 Cr over the same period, only +2.2% YoY. Monthly sales swing
between roughly ₹63 L and ₹1.10 Cr with no single sustained upward or downward trend —
growth is coming in uneven bursts rather than a steady climb.

**Business interpretation:** Margin is being diluted as the business grows. This is
consistent with the discount and category findings below (#5, #3) — more volume is
coming from heavier discounting and a lower-margin product mix, not from selling existing
products more profitably.

**Recommended action:** Set a target of profit growth ≥ sales growth for next year, not
just a sales growth target. Investigate which months/campaigns drove the sales spikes
(e.g., Aug–Sep 2024 and Jun–Aug 2025) to see whether those spikes were discount-driven.

---

### 2. Regional Performance — No region is a problem; South leads narrowly

**Observation:** All four regions perform within a narrow band of each other — there is no
underperforming region requiring intervention.

**Data evidence:** Region totals range from East (~₹5.29 Cr) and West (~₹4.69 Cr) up to
North (~₹5.25 Cr) and South (~₹6.47 Cr, the leader). Profit margin across all four regions
sits between 15.0% and 15.4% — a spread of only 0.4 percentage points. At the state level,
Telangana is the single highest-selling state (₹1.49 Cr).

**Business interpretation:** Regional performance is not a meaningful lever right now —
the business is evenly executed geographically. (Note: the source data tags "Rajasthan" to
both the North and West regions, 196 and 223 orders respectively — see README Assumptions.
This is a data‑mapping quirk, not a sign that the state itself is split in two markets.)

**Recommended action:** Don't prioritize a regional fix. Instead, replicate whatever South
is doing differently (it has the highest sales *and* the highest margin) in onboarding
material for other regional teams, and resolve the Rajasthan region-tagging issue with
whoever owns the source system before the next reporting cycle.

---

### 3. Category / Sub-Category Profitability — Furniture is the clearest margin problem in the business

**Observation:** Furniture sub-categories occupy the four lowest-margin spots in the
entire catalog, far behind Technology and Office Supplies.

**Data evidence:** Bookcases and Tables both run a 5.7% margin; Furnishings 7.9%; Chairs
8.2%. Compare that to Technology's Phones (18.5%), Accessories (18.3%), Copiers (18.0%),
and Machines (18.1%), and Office Supplies' five sub-categories all sitting between 14.2%
and 15.5%. Technology alone contributes the majority of total company profit despite
Furniture having meaningfully higher average discount rates (see #5).

**Business interpretation:** Furniture isn't a small, contained issue — it's a
structurally different (and weaker) business than the other two categories, on both
margin and returns (#7). Sales volume in Furniture is not the problem; profitability per
order is.

**Recommended action:** Review Furniture pricing and supplier cost structure specifically
(not company-wide). Test a smaller, more targeted discount ceiling for Furniture before
applying any company-wide discount policy change.

---

### 4. Customer Segment Behavior — Home Office buys like everyone else but returns more

**Observation:** Home Office is the strongest segment by raw sales and profit, but it also
has the highest return rate of the three segments by a clear margin.

**Data evidence:** Home Office: ₹7.45 Cr sales, 15.5% margin, 5.7% return rate (82 of
1,446 orders returned). Consumer: ₹7.19 Cr sales, 15.3% margin, 3.9% return rate.
Corporate: ₹7.06 Cr sales, 15.2% margin, 4.0% return rate. Home Office's return rate is
about 42–45% higher (relative) than the other two segments, despite all three segments
having essentially the same margin and average order value (~₹50–53K) and rating
(~4.05–4.07 / 5).

**Business interpretation:** Home Office isn't a "bad" segment — it's currently the
top-performing one — but its elevated return rate is a quiet tax on that performance that
doesn't show up in the headline sales number. If left unaddressed, it will compound as
Home Office grows.

**Recommended action:** Pull a sample of Home Office returns and check whether they
cluster in Furniture (likely, given #3) or are a distinct issue (e.g., home-delivery
damage). Confirm before changing any policy specific to this segment.

---

### 5. Discount Impact — Heavy discounting is associated with materially thinner margins

**Observation:** There is a strong, consistent negative relationship between discount
level and profit margin across the whole catalog.

**Data evidence:** Order-level correlation between discount and profit margin is **r =
‑0.60**. By discount bucket, margin falls steadily: 0% discount orders run ~20%+ margin,
while orders discounted 31–35% average roughly ‑5% margin — i.e., the company loses money
on its most heavily discounted orders, on average. The sub-category scatter shows this is
not one outlier: Furniture sub-categories cluster at both the highest average discount
(15–17%) and lowest margin (5.7–8.2%), while Technology sub-categories cluster at the
lowest average discount (11–13%) and highest margin (18%+).

**Business interpretation:** Discounting is not free — past a certain point it isn't just
trading margin for volume, it's actively destroying margin. Furniture's discount-heavy
posture is compounding its already-weak margin structure from #3.

**Recommended action:** Set a margin floor (e.g., no standard discount that pushes
expected margin below 5%) and require manager approval for discounts above ~25%,
especially in Furniture.

---

### 6. Shipping / Delivery Performance — Speed isn't the return-risk driver; ship mode itself is

**Observation:** Faster delivery does not correlate with fewer returns — in fact, the
fastest ship mode (Same Day) has the lowest return rate, while First Class (also
relatively fast) has the highest.

**Data evidence:** By ship mode: Same Day — 0.4 avg days, 2.5% return rate (241 orders);
First Class — 1.8 avg days, 5.1% return rate (630 orders); Second Class — 2.7 avg days,
4.6% return rate (894 orders); Standard Class — 4.7 avg days, 4.6% return rate (2,435
orders, the large majority of volume). Cutting the data by delivery-day buckets instead of
ship mode shows almost no difference in return rate (4.0%–5.1% across all buckets) —
delivery speed itself is not the driver.

**Business interpretation:** The "ship faster to reduce returns" intuition doesn't hold in
this data. First Class's high return rate is most likely about *who* selects First Class
or *what* gets shipped that way, not how long it takes to arrive. Standard Class carries
58% of all order volume, so even its moderate 4.6% return rate has the largest absolute
impact on total returns.

**Recommended action:** Investigate what's specifically driving First Class returns (order
type, customer segment mix, packaging) rather than assuming a delivery-speed fix.
Prioritize any process fix at Standard Class first, given its volume.

---

### 7. Return Pattern — Returns are concentrated in Furniture, not spread evenly

**Observation:** Furniture sub-categories occupy four of the five highest return-rate
spots in the entire catalog.

**Data evidence:** Bookcases (8.4%), Furnishings (8.2%), Chairs (8.0%), and Tables (6.2%)
are all Furniture. The next-highest non-Furniture sub-category, Storage, sits at 4.1% —
roughly half the rate of the top Furniture items. Technology sub-categories are the most
return-safe in the catalog, all between 2.7% and 3.5%. Overall company-wide return rate is
4.5%.

**Business interpretation:** Returns are not a generic "quality control" problem — they're
concentrated in one category, the same category already flagged for weak margin (#3) and
heavy discounting (#5). This triangulates Furniture as the single highest-leverage area
for a focused improvement project.

**Recommended action:** Prioritize a root-cause review of Furniture returns specifically
(damage in transit, sizing/expectation mismatch, product quality) over a company-wide
returns initiative — the data doesn't support a company-wide problem.

---

### 8. Business Risk & Opportunity — Furniture is the single biggest concentrated risk; Technology is the clearest opportunity to double down on

**Observation:** The same category — Furniture — is simultaneously the weakest on margin
(#3), the most heavily discounted (#5), and the most returned (#7). That's a compounding
risk, not three separate small issues. Conversely, Technology is strong on every one of
those same dimensions.

**Data evidence:** Furniture: 5.7–8.2% margin, 15–17% avg discount, 6.2–8.4% return rate
across its four sub-categories. Technology: 18.0–18.5% margin, 11–13% avg discount,
2.7–3.5% return rate across its four sub-categories. Technology alone drives the largest
share of total company profit despite Office Supplies and Furniture together accounting
for a meaningful share of order volume.

**Business interpretation:** **Risk:** Furniture is quietly absorbing margin and
operational cost (returns processing, restocking, discount exposure) for a return that's
far below the rest of the catalog — if Furniture volume grows without a fix, it will drag
down company-wide margin further (consistent with the YoY profit-vs-sales gap in #1).
**Opportunity:** Technology has the headroom to take a larger share of marketing and
inventory investment, since every margin, discount, and return signal points the same
direction in its favor.

**Recommended action:** Leadership should treat Furniture as one connected initiative
(pricing + discount policy + returns root-cause), not three separate workstreams, and
consider shifting incremental marketing/inventory investment toward Technology while that
initiative is underway.

---

## Quick Reference Table

| Area | Headline Number | Risk or Opportunity |
|---|---|---|
| Sales trend | +4.3% YoY sales vs. +2.2% YoY profit | Risk — margin dilution |
| Regional | All regions within 0.4pp margin | Neutral — no regional fix needed |
| Category | Furniture margin 5.7–8.2% vs. Tech 18%+ | Risk — Furniture |
| Segment | Home Office return rate 5.7% vs. 3.9–4.0% others | Watch — Home Office |
| Discount | r = -0.60 discount-to-margin correlation | Risk — deep discounting |
| Shipping | First Class 5.1% return rate, highest of all modes | Watch — First Class |
| Returns | 4 of top 5 return sub-categories are Furniture | Risk — Furniture (compounding) |
| Overall | Furniture weak on margin + discount + returns together | **Top risk: Furniture. Top opportunity: Technology** |
