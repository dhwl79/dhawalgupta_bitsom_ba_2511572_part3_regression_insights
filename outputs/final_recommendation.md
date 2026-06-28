# Final Recommendation

**Based on:** `analysis/regression_workbook.xlsx`, `outputs/regression_summary.xlsx`,
`analysis/model_comparison.md`, `outputs/model_equations.md`, and `analysis/residual_analysis.md`.
Final model: **Multiple Regression 1 (Core)** — R² = 0.82, N = 320 store-months.

## 1. Which factors appear most strongly associated with monthly sales?

In order of strength of evidence:

1. **`footfall`** — by far the strongest association. Alone it explains 74% of the variation in
   monthly sales (simple R² = 0.74), and remains highly significant (p < 0.001) in the full model
   with a coefficient of +₹33.68 per visitor.
2. **`inventory_availability_pct`** — looked weak in isolation but is one of the clearest effects
   once footfall and marketing are controlled for (+₹3,063 per percentage point, p < 0.001).
3. **`marketing_spend`** — significant and actionable, but with a smaller effect than footfall
   (+₹1.18 per ₹1 spent, p < 0.001).
4. **`store_type`** — Airport stores significantly outsell High Street stores (+₹22,958);
   Residential stores significantly underperform them (−₹16,697), holding other factors equal.

## 2. Which variables should leadership focus on?

**Footfall, inventory availability, and marketing spend** — these three, plus store format, make
up the final recommended model and are all backed by strong, consistent statistical evidence
across multiple specifications. Of these, **inventory availability is the most actionable
near-term lever**: it's the kind of operational fix (restocking, supply chain reliability) that's
faster to act on than trying to physically move footfall, and the evidence for it is just as
strong once other factors are accounted for.

## 3. Which variables should NOT be over-interpreted?

- **`avg_discount_pct`** — not statistically significant in any model tested (simple or multiple,
  p ranges from 0.09–0.10 throughout). There's no reliable evidence in this data that discounting
  intensity, by itself, moves monthly sales. Leadership should not assume "discount more" is a
  proven lever based on this analysis.
- **`customer_rating`** — shows essentially zero relationship with sales on its own (simple
  R² = 0.0007, p = 0.63), and only becomes statistically significant once several other variables
  are already in the model (a "suppression" pattern). This is worth a closer, dedicated look, but
  is not strong enough evidence on its own to drive a major customer-experience investment decision
  yet.
- **`store_type_Mall`** — directionally positive but only marginally significant (p ≈ 0.08–0.12
  depending on the model). Treat as a "maybe," not a confirmed effect.

## 4. What business action would you recommend?

1. **Protect and prioritize inventory availability** at stores below the current average (~85%) —
   the model's strongest "operationally fixable" lever with high statistical confidence.
2. **Use footfall as the primary planning input** for sales forecasting and store-level targets,
   since it carries by far the most explanatory power.
3. **Review the Residential store format specifically** — it underperforms equivalent High Street
   stores by ~₹16,700/month even after accounting for footfall, marketing, and inventory. This is
   worth a focused operational review (staffing, local assortment, catchment fit) rather than
   assuming it's simply a "weaker" format.
4. **Investigate the specific stores with the largest negative residuals** (see
   `analysis/residual_analysis.md`) before increasing their marketing budgets further — several of
   them already spend well above average and still underperform their predicted sales, suggesting
   the problem there isn't input *level* but something execution-related the model can't see.
5. **Hold off on a discount-led strategy** until there's better evidence — this analysis doesn't
   support discounting as a reliable sales driver.

## 5. What risks or limitations should leadership keep in mind?

- This is **4 months of data across 80 stores** — enough to find clear patterns, but not enough to
  rule out seasonal effects beyond the single `holiday_flag` indicator.
- **`staff_count` was excluded** from the model because it's almost interchangeable with footfall
  statistically (correlation 0.92) — this does NOT mean staffing doesn't matter, only that this
  dataset can't cleanly separate its effect from footfall's.
- **`region` was not included** in the final model. The residual analysis shows a real, modest
  pattern by region (East stores average ~₹10,800 below prediction; South stores average ~₹9,300
  above) that the current model doesn't explain — a useful next step, not a flaw to ignore.
- **Average residual size is ~₹44,000** — meaningful individual-store predictions should be read
  with that margin of uncertainty in mind, not treated as exact.

## 6. Why does regression show association, not causation?

Regression measures how strongly variables move together across the stores and months in this
dataset — it does not establish that one *causes* the other. Three concrete reasons that matters
here:

- **Reverse causation is plausible.** A well-performing store may *attract* more marketing budget
  *because* it's already doing well, rather than the spend causing the sales. The data alone can't
  tell these two stories apart.
- **Omitted variables could explain both.** A great store manager could independently drive both
  higher footfall and higher inventory discipline — in that case footfall and inventory would
  appear linked to sales, when the real driver is management quality, which isn't in this dataset
  at all.
- **No randomization occurred.** No store was randomly assigned a marketing budget, discount level,
  or inventory target — every value in this dataset reflects decisions already made for reasons
  that may themselves correlate with sales. Without an experiment (e.g. randomly increasing
  marketing spend at a sample of stores and measuring the effect), the *size* of any of these
  coefficients should be treated as a strong clue for where to investigate and test, not as a
  guaranteed return on investment.

**Bottom line:** this analysis is strong evidence for *where to focus attention* (footfall,
inventory availability, marketing spend, store format) — it is not, on its own, proof that pulling
any one of those levers will move sales by exactly the modeled amount. The recommended next step is
to test the highest-confidence, most actionable lever (inventory availability) in a controlled way
at a subset of stores before rolling out a chain-wide change.
