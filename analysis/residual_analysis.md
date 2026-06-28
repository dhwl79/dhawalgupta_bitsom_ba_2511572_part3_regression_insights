# Residual Analysis

**Final model used:** Multiple Regression 1 (Core) —
`monthly_sales ~ footfall + marketing_spend + inventory_availability_pct + store_type dummies`
(reference category = High Street). See `outputs/model_equations.md` for the full equation and
`analysis/regression_workbook.xlsx`, sheet `Predictions_Residuals`, for the live calculation across
all 320 store-months.

## 1–2. How predicted sales and residuals were calculated

For every store-month:

```
predicted_sales = Intercept + b1×footfall + b2×marketing_spend + b3×inventory_availability_pct
                  + b4×(store_type = Mall) + b5×(store_type = Residential) + b6×(store_type = Airport)

residual = monthly_sales (actual) − predicted_sales
```

All six coefficients are pulled live from the `Multiple_Regression` sheet, so the residual table
recalculates automatically if the model is refit. Overall residual standard deviation: **≈ 44,036**
(i.e. predictions are typically within roughly ±44K of actual sales).

## 3. Top 5 largest POSITIVE residuals (model under-predicts these)

| store_id | month | region | store_type | Actual Sales | Predicted | Residual |
|---|---|---|---|---|---|---|
| STR-1073 | 2025-03 | East | Residential | 813,316.71 | 707,767.97 | **+105,548.74** |
| STR-1030 | 2025-02 | West | Residential | 820,519.04 | 715,770.95 | **+104,748.09** |
| STR-1028 | 2025-04 | East | Mall | 713,611.16 | 614,751.11 | **+98,860.05** |
| STR-1032 | 2025-01 | South | High Street | 914,544.17 | 815,726.57 | **+98,817.60** |
| STR-1050 | 2025-04 | North | Residential | 735,786.64 | 642,285.15 | **+93,501.49** |

## 4. Top 5 largest NEGATIVE residuals (model over-predicts these)

| store_id | month | region | store_type | Actual Sales | Predicted | Residual |
|---|---|---|---|---|---|---|
| STR-1017 | 2025-03 | West | High Street | 685,379.08 | 844,194.64 | **−158,815.56** |
| STR-1023 | 2025-02 | South | Mall | 627,171.90 | 749,860.67 | **−122,688.77** |
| STR-1012 | 2025-01 | West | Residential | 595,467.60 | 713,439.74 | **−117,972.14** |
| STR-1007 | 2025-02 | West | Mall | 800,451.94 | 902,543.28 | **−102,091.34** |
| STR-1009 | 2025-01 | North | Residential | 641,865.03 | 743,585.50 | **−101,720.47** |

## 5. What these residuals may mean in business terms

- **Positive residuals (sold more than the model expected)** describe stores that are outperforming
  what their footfall, marketing spend, inventory availability, and format alone would predict.
  This points to something the model doesn't measure — strong local store management, an unusually
  loyal customer base, a weak nearby competitor, or an effective local promotion not captured by
  `avg_discount_pct`. These stores are good candidates to study as **internal best-practice examples**.

- **Negative residuals (sold less than the model expected)** are more concerning from a spend-efficiency
  angle: **4 of the 5 largest negative residuals belong to stores with marketing spend well above the
  320-store average** (₹79K–₹172K vs. an overall average of ~₹56K), yet they still underperformed their
  predicted sales. That combination — high spend, high footfall/inventory, but a big sales shortfall —
  suggests the issue at these specific stores likely isn't the *level* of the standard inputs, but
  something execution- or location-specific the model can't see (in-store experience, stock-out timing,
  local competition, staffing quality on the shop floor, etc.).

- The single largest miss in either direction, **STR-1017 (−158,816)**, had high footfall (9,628),
  near-full inventory availability (99%), and above-average marketing spend (₹79,346) — on paper, an
  ideal setup — yet sold far below prediction. This is the strongest single candidate for a manual
  investigation (data entry error, a one-off local disruption, or a genuine operational problem).

## 6. Is the model systematically under- or over-predicting certain types of stores?

- **By `store_type`: no systematic bias.** Because `store_type` dummies are included as predictors,
  the average residual within every store type is essentially zero by construction (High Street,
  Mall, Residential, and Airport all average out to ~0). What does differ is the *spread* —
  Residential stores have the widest spread of residuals (std ≈ 46,930) and High Street the
  narrowest (std ≈ 41,136), meaning Residential store performance is harder to predict from these
  inputs alone, even though there's no overall up/down bias.

- **By `region`: a real, unexplained pattern exists.** `region` was *not* included in the final
  model, and the residuals show it still matters somewhat:

  | Region | Average residual |
  |---|---|
  | East | **−10,779** (model over-predicts East on average) |
  | North | −2,605 |
  | West | +7,916 |
  | South | **+9,325** (model under-predicts South on average) |

  This is a modest but real gap of roughly ₹20K between South and East on average. It suggests
  region carries some genuine signal beyond what footfall/marketing/inventory/store_type already
  capture — a reasonable next step would be a Model 3 that adds region dummies, traded off against
  the added complexity of more dummy variables in an already-strong model.
