# Model Equations

## Dummy variable approach

`store_type` has 4 categories: High Street (116 of 320 rows), Residential (100), Mall (76), and
Airport (28). Using all 4 as dummy columns would create perfect redundancy (the **"dummy variable
trap"**) — the 4 columns would always sum to 1 for every row, making them perfectly collinear with
the model's intercept and breaking the regression. So we create only **3** dummy columns:

- `store_type_Mall` = 1 if store_type is Mall, else 0
- `store_type_Residential` = 1 if store_type is Residential, else 0
- `store_type_Airport` = 1 if store_type is Airport, else 0

**Reference category: High Street** (chosen because it's the most frequent category — the most
stable baseline to compare everything else against). High Street's effect is absorbed into the
model's intercept; every dummy coefficient is read as *"the difference from a High Street store
with the same footfall, marketing spend, and inventory availability."*

The same logic was applied to `region` (3 dummies — West, North, South — with East as the reference,
again the most frequent category) and is available in `analysis/regression_workbook.xlsx`, sheet
`Dummy_Variables`, for completeness, even though the final selected model uses `store_type` dummies
only (region was tested informally but not included in the final model — see Limitations below and
`analysis/residual_analysis.md`).

## Simple regression equations

| # | Equation | R² | Significant? |
|---|---|---|---|
| 1 | `monthly_sales = 446,410.58 + 35.6780 × footfall` | 0.7363 | Yes (p < 0.001) |
| 2 | `monthly_sales = 560,777.35 + 2.1296 × marketing_spend` | 0.1672 | Yes (p < 0.001) |
| 3 | `monthly_sales = 697,835.63 − 138,730.45 × avg_discount_pct` | 0.0083 | No (p = 0.104) |
| 4 | `monthly_sales = 484,814.26 + 2,217.83 × inventory_availability_pct` | 0.0131 | Borderline (p = 0.041) |
| 5 | `monthly_sales = 702,011.82 − 5,448.36 × customer_rating` | 0.0007 | No (p = 0.627) |

## Multiple regression equation (Model 1 — Core, the FINAL selected model)

```
monthly_sales = 123,291.89
                + 33.6836 × footfall
                + 1.1767  × marketing_spend
                + 3,062.93 × inventory_availability_pct
                + 11,651.28 × store_type_Mall
                − 16,696.67 × store_type_Residential
                + 22,957.90 × store_type_Airport
```

R² = 0.8199, Adjusted R² = 0.8165, N = 320. All coefficients are statistically significant at the
5% level except `store_type_Mall` (p = 0.078, marginal).

### Explanation of each coefficient

- **Intercept (123,291.89):** the model's baseline prediction for a High Street store with
  footfall = 0, marketing spend = 0, and inventory availability = 0%. This is a mathematical
  anchor point, not a realistic real-world scenario (no real store has zero footfall) — it should
  not be interpreted on its own.
- **footfall (+33.68):** holding marketing spend, inventory availability, and store type constant,
  each additional monthly visitor is associated with about +₹33.68 in monthly sales. This is the
  single strongest, most reliable driver in the dataset.
- **marketing_spend (+1.18):** holding the other factors constant, each additional ₹1 of monthly
  marketing spend is associated with about +₹1.18 in monthly sales. Still positive and significant
  once footfall is controlled for, though the effect is smaller than in the simple regression
  (₹2.13) — some of marketing's apparent effect on its own was really working *through* footfall.
- **inventory_availability_pct (+3,062.93 per percentage point):** holding the other factors
  constant, each extra percentage point of product availability is associated with about
  +₹3,063 in monthly sales. This variable looked weak alone (Simple Model 4) but becomes one of
  the clearest effects in the multiple regression — once footfall/marketing differences between
  stores are accounted for, inventory's true relationship with sales becomes visible.
- **store_type_Mall (+11,651, marginal):** a Mall store is predicted to sell about ₹11,651 more
  per month than a High Street store with the same footfall/marketing/inventory profile — but the
  evidence isn't quite strong enough (p = 0.078) to treat this as reliable on its own.
- **store_type_Residential (−16,697, significant):** a Residential store sells about ₹16,697
  *less* per month than an equivalent High Street store, holding the other factors constant — a
  real, statistically reliable gap.
- **store_type_Airport (+22,958, significant):** an Airport store sells about ₹22,958 *more* per
  month than an equivalent High Street store, holding the other factors constant — the largest
  store-format effect in the model, and statistically reliable despite Airport being the smallest
  group (28 of 320 rows).

## Final model selected and why

**Multiple Regression 1 (Core)** was selected as the final model over both the simple regressions
and the Extended multiple regression, because:

1. It explains nearly as much variation as the Extended model (R² 0.8199 vs 0.8258) using **two
   fewer variables** — a better trade-off between accuracy and simplicity.
2. Every numerical predictor in it is highly significant (p < 0.001); it doesn't lean on any
   variable whose evidence is weak.
3. `avg_discount_pct`, the variable the Extended model adds first, is **not** statistically
   significant in either specification (p ≈ 0.09–0.10) — including it wouldn't be supported by
   the evidence.
4. `customer_rating` becomes significant in the Extended model, which is a genuinely interesting
   finding (see `analysis/residual_analysis.md` and `outputs/final_recommendation.md`), but because
   that significance only appears once several other variables are already in the model, it's a
   less robust kind of evidence than a variable that's significant on its own — better suited to a
   "worth investigating further" recommendation than as a pillar of the headline business model.
