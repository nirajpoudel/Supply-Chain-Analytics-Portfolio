# P0 — Exploratory Data Analysis
**M5 Forecasting Dataset · FOODS Department · Walmart CA_1 Store**

---

## Overview

Exploratory Data Analysis (EDA) is the mandatory first step before any forecasting, planning, or optimization work begins. You cannot build a reliable demand forecast on data you have not interrogated. You cannot set a safety stock level without knowing how erratic demand actually is. You cannot plan promotions or holiday ordering without quantifying how events shift sales.

This project performs a complete EDA on **355 days of daily unit sales** (January 29, 2011 – January 18, 2012) for **three FOODS department SKUs** at a single California Walmart store — using nothing but Microsoft Excel. It is structured as eight dedicated analytical sheets, each answering a distinct question about the data, and collectively building the full picture a supply chain analyst needs before touching a model.

---

## Dataset

| File | Description |
|---|---|
| `sales_train_validation.csv` | M5 Competition — 30,490 SKUs × 1,913 daily sales columns |
| `calendar.csv` | Date dimension — weekday, month, events, SNAP flags, Walmart week IDs |
| **Scope** | SKUs: `FOODS_1_001`, `FOODS_1_002`, `FOODS_1_003` · Store: `CA_1` · Days: `d_1` → `d_355` |

Raw data was extracted using **Power Query** (filtered a 30,490-row × 1,919-column flat file to 3 target rows) and joined to the calendar dimension using **INDEX+MATCH** for horizontal-to-vertical transposition across sheets.

---

## Workbook Structure

### Sheet 1 — RawData
**What it contains:** The clean, static base table. 355 rows × 15 columns: day index (`d`), date, Walmart week ID, weekday text, weekday number, month, year, event name, event type, SNAP flag for California, and daily unit sales for all three SKUs.

**Why it matters:** Every analysis sheet in this workbook references RawData as a single source of truth. Keeping it as a paste-values static copy (not live formulas) protects against accidental overwrites and makes the workbook self-contained — a data hygiene principle that matters in any professional analytics environment.

**Concepts covered:** Data extraction, Power Query filtering, multi-source data joining, column standardization, static vs. live references.

---

### Sheet 2 — SummaryStats
**What it contains:** A full descriptive statistics profile for each SKU — total units sold, average daily sales, median, standard deviation, Coefficient of Variation (CV), min, max, zero-sales day count, zero-sales rate, peak day, peak date, 25th percentile, 75th percentile, and IQR.

**Why it matters:** This is where you classify the demand profile before committing to any forecasting method. The single most important metric here is the **Coefficient of Variation (CV = Std Dev ÷ Mean)**. All three SKUs have a CV above 1.2 — well above the 0.5 threshold that defines highly intermittent demand. Over 50% of days record zero sales across all three SKUs. This immediately rules out simple moving averages and basic exponential smoothing as appropriate methods. In a real business context, misclassifying intermittent demand as regular demand leads to chronic overstock, capital tied up in slow-moving inventory, and frequent write-offs — or the opposite: stockouts on the rare high-demand days when customers actually need the product.

The **IQR and percentile profile** completes the picture: when demand does occur, it mostly falls in the 1–2 unit range. The occasional single-day spikes (max of 9 units for SKU1) are real outliers, not the norm.

**Concepts covered:** Descriptive statistics, demand classification, Coefficient of Variation, intermittent demand identification, outlier detection, percentile analysis.

---

### Sheet 3 — WeekdayPattern
**What it contains:** Average daily sales per SKU broken down by day of week (Saturday through Friday, following Walmart's week convention where Saturday = day 1). Includes a **Seasonal Index** row for each day — calculated as that day's average divided by the overall average.

**Why it matters:** Demand is not flat across the week in retail. Understanding which days consistently over- or under-perform the weekly average is foundational to several real business decisions: staffing and labor scheduling, delivery frequency planning, promotional timing, and short-term replenishment triggers. The seasonal index turns a raw average into a relative multiplier — an index of 1.31 on Sunday means Sundays sell 31% above the weekly average. This same index structure is what analysts plug into decomposition-based forecasting models to separate the day-of-week effect from the underlying demand level.

Each SKU shows a distinct weekday signature, which is itself an insight: these three items in the same department at the same store do not behave identically, meaning a category-level replenishment rule would systematically mis-serve at least one of them.

**Concepts covered:** AVERAGEIF for conditional aggregation, seasonal index construction, day-of-week decomposition, demand segmentation, application to labor planning and replenishment cadence.

---

### Sheet 4 — MonthlyPattern
**What it contains:** Average daily sales per SKU by calendar month (January through December), with a **Monthly Seasonal Index** for each SKU.

**Why it matters:** Within-year seasonality is one of the most important — and most frequently underestimated — variables in demand planning. A business that plans January inventory using December's average will overstock. One that plans August ordering using May's numbers will overstock in a completely different direction. The monthly index makes the seasonal pattern explicit and usable: an analyst can take a baseline forecast and multiply it by the monthly index to produce a seasonally-adjusted plan.

This sheet also surfaces an analytically important anomaly: FOODS_1_001 shows near-zero sales in August through October — a collapse that deserves investigation. Is it a ranging or listing change? A stockout that was never replenished? True demand dropout? Identifying this kind of anomaly during EDA is exactly what prevents a forecasting model from training on corrupted signal.

**Concepts covered:** AVERAGEIF by month, monthly seasonal index construction, within-year seasonality, anomaly identification, seasonally-adjusted demand planning.

---

### Sheet 5 — EventAnalysis
**What it contains:** Three connected analyses. First, average daily sales split by event type (No Event, Sporting, Cultural, National, Religious) with counts of each. Second, **Event Lift %** — how much each event type shifts sales above or below the no-event baseline. Third, an individual event lookup table listing every named calendar event in the 355-day window with the corresponding sales figure on that day.

**Why it matters:** In real retail supply chain, calendar events are treated as **known demand shifters** — external factors that a statistical model trained on historical averages will miss unless explicitly encoded. National holidays (Memorial Day, Independence Day, Labor Day, Thanksgiving, Christmas) show consistent negative lift across all three SKUs, meaning demand suppresses on public holidays in this category. Sporting events show strong positive lift for SKU1 and SKU3. This is not a coincidence — it is a signal about what these products are and when people buy them.

The practical output of this sheet is the event lift factor, which feeds directly into demand planning adjustments: if a forecast says you need 10 units in a week containing a National holiday, the -46% lift on SKU1 means you should plan for closer to 6. Getting this wrong in the other direction — not adjusting and ordering the full 10 — is how holiday overstock accumulates.

**Concepts covered:** AVERAGEIF/COUNTIF for event segmentation, lift calculation vs. baseline, external demand driver quantification, calendar effect modeling, promotional and holiday order adjustment logic.

---

### Sheet 6 — SNAPAnalysis
**What it contains:** Average daily sales on SNAP days vs. non-SNAP days for each SKU, with SNAP uplift percentage. Also a secondary breakdown showing how SNAP days distribute across weekdays in California, and average sales for each SNAP-weekday combination.

**Why it matters:** SNAP (Supplemental Nutrition Assistance Program) is a US government food assistance program that disburses benefits at set times each month. For food retailers, SNAP disbursement dates create **predictable, cyclical demand spikes** that a model trained on raw daily averages will smooth over. At CA_1, SNAP days generate roughly 9–15% higher sales for SKU1 and SKU2. In a real supply chain context, this means replenishment orders should be front-loaded before anticipated SNAP disbursement windows — the same way retailers stock up before weekends.

The secondary weekday-SNAP interaction analysis is important because it shows that SNAP uplift is not uniform across days: the combination of a SNAP day falling on a high-index weekday compounds the effect, while a SNAP day on a low-index weekday dampens it. An analyst who only looks at "SNAP vs. non-SNAP" misses this interaction.

**Concepts covered:** AVERAGEIF with binary flags, uplift calculation, government program demand drivers, COUNTIFS/AVERAGEIFS for two-variable interaction analysis, demand driver interaction effects.

---

### Sheet 7 — RollingTrend
**What it contains:** Daily sales for all three SKUs alongside a **28-day (4-week) rolling average** and 28-day rolling total for SKU1, charted as actual daily sales (thin line) over the rolling average (thick smoothed line).

**Why it matters:** Raw daily sales data for intermittent items is too noisy to read trend from directly. A single high day can look like a recovery; a single zero can look like a collapse. The rolling average smooths out day-to-day randomness and reveals the actual underlying demand trend over time. This is how analysts determine whether demand is growing, flat, or declining — which drives decisions about range investments, reorder point adjustments, and whether a slow period is a trend or just noise.

For these three SKUs, the rolling average shows that demand is roughly stationary over the year with seasonal oscillation — there is no strong secular trend either upward or downward. That is itself a usable finding: it means a trend-adjusted forecasting model (Holt-Winters double exponential smoothing, for example) would add unnecessary complexity without improving accuracy.

**Concepts covered:** Rolling window calculations, noise reduction, trend identification, stationarity assessment, chart design for time series communication.

---

### Sheet 8 — CorrelationMatrix
**What it contains:** A 3×3 Pearson correlation matrix between the three SKU daily sales series, plus a demand variability ranking using the CV values from SummaryStats.

**Why it matters:** Correlation between SKUs in the same department matters for two distinct reasons. High correlation means the SKUs share demand drivers — they respond similarly to events, SNAP days, and weekday patterns. This is useful because it validates that the patterns found in earlier sheets apply across the category, not just to one item. It also has implications for inventory pooling: if two SKUs are highly correlated and serve similar demand occasions, a retailer might evaluate whether both need to be ranged simultaneously, or whether one partially substitutes for the other.

The **demand variability ranking** gives a clean comparative output: which SKU is the most stable (easiest to forecast), which is the most erratic (requires the most safety stock buffer and the most sophisticated model). This ranking is the logical entry point for prioritizing which item to focus analytical resources on in Projects 2 through 5.

**Concepts covered:** Pearson correlation, CORREL function, inter-series relationship analysis, demand variability ranking, SKU prioritization for forecasting and inventory investment.

---

## Skills Demonstrated

**Data Engineering in Excel**
- Power Query: extracting 3 target rows from a 30,490-row × 1,919-column flat file without loading the full dataset into memory
- INDEX+MATCH for horizontal-to-vertical data transposition (sales columns across → one row per day)
- Multi-sheet relational data model with a single RawData source feeding all analysis sheets

**Statistical Analysis**
- Full descriptive statistics profile including CV, IQR, zero-sales rate, and percentile boundaries
- Demand classification using CV thresholds
- Pearson correlation and variability ranking

**Demand Pattern Analysis**
- Seasonal index construction at weekday and monthly granularity
- Event type lift calculation vs. no-event baseline
- SNAP program uplift analysis with two-variable weekday interaction
- 28-day rolling average for trend isolation

**Analytical Interpretation**
- Correctly classified all three SKUs as intermittent demand (CV > 1.0) rather than applying standard forecasting approaches
- Identified August–October anomaly in SKU1 as a flag for investigation before any model training
- Distinguished SKU-level behavioral differences within the same department and store
- Connected every analytical output to a downstream business or modeling decision

---

## Tools

- **Microsoft Excel** — Power Query, INDEX+MATCH, AVERAGEIF / AVERAGEIFS / COUNTIF / COUNTIFS, CORREL, PERCENTILE, STDEV, conditional formatting, line and bar charts
- **M5 Forecasting Dataset** — Walmart retail sales data (Makridakis et al., public competition dataset via Kaggle)
- No Python. No Power BI. No third-party add-ins.

---

---

*This project is part of the [Floor to Forecast Roadmap](https://nirajpoudel.com) — a structured portfolio series mapping the journey from floor to supply chain data analyst.*