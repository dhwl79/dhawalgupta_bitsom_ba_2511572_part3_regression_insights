# Chart Selection Justification

For each major view on the dashboard: the question it answers, why that chart type fits,
what's mapped to which encoding, the design principle applied, and the mistake it
deliberately avoids.

---

## 1. Sales Trend (Line Chart)

- **Question answered:** How is sales performing over time, and is the business growing?
- **Why this chart type:** Line charts are the standard, least-ambiguous way to show a
  continuous measure changing over a continuous time axis. Any other chart type (bars per
  month, for instance) would work but adds visual weight without adding clarity for a
  single continuous trend.
- **Encoding:** Columns = Order Date (continuous, truncated to Month); Rows = SUM(Sales);
  no color encoding (a single series doesn't need one — adding color here would be
  decoration, not information).
- **Design principle applied:** *Minimal clutter / appropriate chart for the question.* A
  reference line for the average is included so leadership can see above/below-average
  months at a glance without needing to mentally compute it.
- **Mistake avoided:** Truncating the y-axis to make growth look more dramatic than it is.
  The axis starts at ₹0, so the real proportional size of each month-to-month swing is
  honestly represented.

## 2. Regional & State Performance (Bar Chart)

- **Question answered:** Which region/state performs best, and is any region a problem?
- **Why this chart type:** A sorted horizontal bar chart is the most accurate way to
  compare a ranked list of ~19 categorical values — length is the easiest visual variable
  for humans to compare precisely, more so than angle (pie) or area (treemap) for this
  many categories.
- **Encoding:** Rows = State (sorted descending by Sales); Columns = SUM(Sales); Color =
  Region (4 categorical colors), which lets the same chart answer both "which state" and
  "which region" questions at once without needing two separate charts.
- **Design principle applied:** *Appropriate sorting.* Bars are sorted by value, not
  alphabetically — alphabetical sorting would force the reader to scan the whole chart to
  find the top performer instead of reading it off the top row.
- **Mistake avoided:** Using a geographic map for only 4 regions / ~19 states with no
  further geographic drill-down value to add. A map looks impressive but a sorted bar
  chart is actually faster to read accurately here, and avoids the misleading visual where
  a state's *map area* (which varies by physical size, not sales) competes with its actual
  sales for the reader's attention.

## 3. Category & Sub-Category Profitability (Bar Chart, Diverging Color)

- **Question answered:** Which categories and sub-categories drive profit — and which
  drag it down?
- **Why this chart type:** Bar length for the absolute profit number, combined with a
  diverging color scale for margin, lets the chart answer two related-but-different
  questions ("how much profit" and "how efficient was that profit") in one view instead of
  forcing a choice between them.
- **Encoding:** Rows = Category → Sub-Category (a two-level hierarchy, grouped); Columns =
  SUM(Profit); Color = Profit Margin (calculated field) on a red→yellow→green diverging
  scale.
- **Design principle applied:** *Clear hierarchy.* Sub-categories are nested under their
  parent category rather than flattened into one alphabetical list of 13 items, so the
  Furniture/Office Supplies/Technology pattern is visible as a group, not just as
  scattered low bars the reader has to mentally re-sort.
- **Mistake avoided:** Using a single sequential color scale (e.g., light-to-dark blue) for
  margin, which would not visually flag "this is bad" the way red does. A diverging scale
  centered near a reasonable margin level makes the Furniture problem visually jump out
  without reading a single number.

## 4. Customer Segment Scorecard (Highlight Table)

- **Question answered:** How do the three customer segments compare across the metrics
  leadership cares about, in one place?
- **Why this chart type:** A highlight table (color-coded text table) is explicitly
  suited to "compare a few categories across several metrics simultaneously" — better
  than 6 separate bar charts, because it lets a reader scan one row to get a complete
  segment profile.
- **Encoding:** Rows = Customer Segment; Columns = Sales, Profit, Margin, AOV, Return Rate,
  Avg Rating; Color = conditional per column (green = better, red = worse for that
  column's direction — return rate is the one column where "high" is colored as a
  warning, not an achievement).
- **Design principle applied:** *Consistent color usage with an intentional exception.*
  Every column uses green-for-good, except Return Rate, which inverts the logic
  deliberately (low is good) — this is flagged so the exception is a design choice, not an
  inconsistency.
- **Mistake avoided:** Coloring Return Rate the same direction as the other columns (i.e.,
  green = high), which would visually reward the segment with the *worst* return
  performance — a genuinely common dashboard design bug.

## 5. Shipping Performance (Bar Chart, Color-Coded)

- **Question answered:** Which shipping mode is slow, and which carries return risk?
- **Why this chart type:** A simple bar chart ranks four categories on one primary
  measure (delivery days) while color carries a second measure (return rate) — appropriate
  per the brief's own suggested mapping ("bar chart or table" for shipping-mode
  questions).
- **Encoding:** Columns = Ship Mode; Bar height = Avg. Delivery Days; Color = Return Rate.
- **Design principle applied:** *Focus on business interpretation over raw display.*
  Labels show both the delivery-day number and the return-rate percentage directly on the
  chart, so the reader doesn't have to cross-reference a legend to get the two numbers
  that matter.
- **Mistake avoided:** Letting bar height also represent return rate (a second, unrelated
  measure) which would force a dual-axis chart — a well-known source of misleading
  comparisons when two measures with different scales are graphed on the same axis.

## 6. Discount vs. Profit (Scatter Plot)

- **Question answered:** How does discount level relate to profitability?
- **Why this chart type:** Scatter plots are the standard chart for showing the
  relationship between two continuous measures — exactly the brief's own suggested
  mapping for this question.
- **Encoding:** X = Average Discount; Y = Profit Margin; one mark per Sub-Category
  (aggregated, not all 4,200 raw orders, to keep the relationship readable); Size = Sales
  (so a reader can see whether the pattern is being driven by large or small
  sub-categories); Color = Category.
- **Design principle applied:** *Avoidance of misleading scales / overplotting.* Plotting
  4,200 raw points would create an unreadable cloud where the real relationship is hidden
  by point density; aggregating to 13 sub-category points with a trend line keeps the
  negative relationship visible and honest, while size still hints at the underlying
  volume.
- **Mistake avoided:** Drawing a trend line through the origin or forcing the axes to start
  at zero, which would compress the actual data range. Axes are scaled to the data's real
  range so the slope of the relationship isn't visually flattened or exaggerated.

## 7. Return Analysis (Bar Chart, Sorted Descending)

- **Question answered:** Which products get returned the most, and is the problem
  concentrated or spread out?
- **Why this chart type:** A sorted bar chart, same logic as #2 — precise ranked
  comparison across 13 sub-categories, with a reference line for the company-wide average
  so each bar's distance from "normal" is immediately visible.
- **Encoding:** Rows = Sub-Category (sorted descending by Return Rate); Columns = Return
  Rate; Color = Category.
- **Design principle applied:** *Readable titles / clear labels.* The subtitle states the
  takeaway in plain language ("returns are concentrated in one category") rather than
  leaving the reader to infer it — a dashboard for leadership should lead with the
  interpretation, not just the data.
- **Mistake avoided:** Sorting alphabetically or by category instead of by the metric in
  question, which would scatter the four worst-performing Furniture sub-categories apart
  from each other and hide the clustering pattern that is the entire point of this chart.

## 8. KPI Cards (Big Number / Text)

- **Question answered:** What are the headline numbers, before looking at any detail?
- **Why this chart type:** A single bold number with a trend indicator is the correct,
  minimal way to show "the answer" to a simple question (what's our total sales/profit/
  margin/return rate) — anything more elaborate (a small embedded chart, for instance)
  would compete with the detail views below it for attention.
- **Encoding:** Label = the aggregated measure (SUM(Sales), SUM(Profit), Profit Margin
  calculated field, Return Rate calculated field); no color/size encoding beyond the
  card's accent border, which exists only to visually separate the four cards.
- **Design principle applied:** *Hierarchy.* KPI cards sit at the very top of the
  dashboard, above every chart, establishing visual hierarchy: headline numbers first,
  supporting detail below.
- **Mistake avoided:** Cramming a sparkline or secondary metric into every KPI card. Five
  KPI cards each showing two competing pieces of information would slow down the "glance
  and absorb" reading style a KPI row is supposed to support.

## Cross-Cutting Notes

- **Color is reused consistently across the whole dashboard**: Category colors (Furniture
  = red-toned, Office Supplies = blue, Technology = green) and Region colors are fixed
  globally, so the same color always means the same category/region everywhere it
  appears — a reader who learns "red = Furniture" on one chart doesn't have to relearn it
  on the next.
- **Every chart's title states the business question or finding in plain language**,
  not just the field names being plotted (e.g., "Regional & State Performance" rather than
  "SUM(Sales) by State"), per the brief's "business-friendly formatting" requirement.
- **No 3D effects, no unnecessary pie charts, and no dual-axis combinations** appear
  anywhere on this dashboard — all three are common sources of distorted or hard-to-compare
  data and were deliberately avoided throughout.
