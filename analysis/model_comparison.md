# Model Comparison

All figures below are taken directly from the live formulas in `analysis/regression_workbook.xlsx`
(sheets `Simple_Regression`, `Multiple_Regression`, and `Model_Comparison`) and independently
reproduced in `outputs/regression_summary.xlsx`. Both files agree exactly.

Dependent variable for every model: **`monthly_sales`**.

| Model | Independent Variable(s) | N | R-squared | Adj. R-squared | Significant variables (p < 0.05) | Business usefulness | Limitations |
|---|---|---|---|---|---|---|---|
| **Simple 1** | `footfall` | 320 | 0.7363 | n/a (1 predictor) | `footfall` (p < 0.001) | High — footfall alone explains ~74% of the variation in sales. Best single early-warning indicator. | Doesn't tell leadership *how* to move footfall (marketing? location?), and ignores every other driver. |
| **Simple 2** | `marketing_spend` | 320 | 0.1672 | n/a | `marketing_spend` (p < 0.001) | Moderate — significant and directly actionable (it's a lever leadership controls), but explains only ~17% of variation alone. | Says nothing about diminishing returns or the right spend level; doesn't control for store size/footfall. |
| **Simple 3** | `avg_discount_pct` | 320 | 0.0083 | n/a | None — p = 0.104 | Low — no reliable evidence that discounting alone predicts sales. | Coefficient is large and negative, which could mislead if read without the p-value; sample alone can't separate discounting from other causes. |
| **Simple 4** | `inventory_availability_pct` | 320 | 0.0131 | n/a | `inventory_availability_pct` (p = 0.041, borderline) | Low alone, but see Multiple 1 — once other factors are controlled for, this variable strengthens considerably. | Barely significant in isolation; on its own it would be easy to wrongly dismiss this variable. |
| **Simple 5** | `customer_rating` | 320 | 0.0007 | n/a | None — p = 0.627 | Very low — no linear relationship with sales detectable on its own. | See Multiple 2: this variable's relationship only appears once other variables are controlled for (a "suppression" pattern), so a simple regression alone is the wrong tool to evaluate it. |
| **Multiple 1 (Core)** | `footfall`, `marketing_spend`, `inventory_availability_pct`, `store_type` dummies (Mall, Residential, Airport; ref = High Street) | 320 | **0.8199** | **0.8165** | All except `store_type_Mall` (p = 0.078, marginal) | **High — the strongest model that stays fully interpretable.** Explains ~82% of sales variation with variables leadership can act on or plan around. | store_type effects are relative to High Street only; doesn't include region, discounting, or rating. |
| **Multiple 2 (Extended)** | Model 1 + `avg_discount_pct`, `customer_rating` | 320 | 0.8258 | 0.8213 | All except `avg_discount_pct` (p = 0.091) and `store_type_Mall` (p = 0.122) | Medium-high — only a marginal R-squared gain (+0.006) for 2 extra variables; the `customer_rating` finding is genuinely interesting but should be treated cautiously (see below). | Adding variables that are individually weak makes the model harder to act on for a small accuracy gain; `customer_rating`'s significance is sensitive to which other variables are included (a suppression effect), which is a less robust kind of evidence. |

## Final model selected: **Multiple 1 (Core)**

It captures almost all of the Extended model's explanatory power (0.8199 vs 0.8258 R-squared) with two
fewer variables, keeps every numerical predictor highly significant, and avoids leaning on
`avg_discount_pct`, which is not significant in either multiple-regression specification. Full
reasoning is in `outputs/model_equations.md`.

## What none of these models capture (general limitations)

- **All models are observational, not experimental** — no variable was randomly assigned, so none of
  these results prove causation (see `outputs/final_recommendation.md` for a full discussion).
- **`staff_count` was deliberately excluded** from every multiple regression because it correlates
  0.92 with `footfall` (confirmed by a variance inflation factor of ~6.4 when both are included) —
  including both would make their individual coefficients unstable and misleading.
- **`region` was not included** in the final model, even though dummy variables for it were created
  (see `analysis/regression_workbook.xlsx`, sheet `Dummy_Variables`). The residual analysis shows a
  small region-based pattern as a result — see `analysis/residual_analysis.md`.
- **Only 4 months of data** (Jan–Apr 2025) are available, so no model here captures seasonality beyond
  the `holiday_flag` indicator.
