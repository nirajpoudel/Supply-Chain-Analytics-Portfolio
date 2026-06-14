# P0 — Exploratory Data Analysis
**M5 Forecasting Dataset · FOODS Department · Walmart CA_1 Store**

---

## Overview

Before you build any forecast, before you set a single reorder point, before you touch a model — you need to understand your data. What does demand actually look like? Is it smooth or erratic? Does it spike on weekends? Do holidays help or hurt sales? Does the government assistance program in your state move the needle?

These are not optional questions. They are the difference between a forecast that reflects reality and one that confidently produces the wrong number.

This project is a complete exploratory analysis of daily sales data for three food items at a Walmart store in California — using 355 days of real transaction data from the M5 Forecasting Competition. No Python. No Power BI. Just Excel, done properly.

The goal is to know these three SKUs inside out before anything gets modeled.

---

## Dataset

| File | What it is |
|---|---|
| `sales_train_validation.csv` | M5 Competition file — 30,490 SKUs, each with 1,913 days of daily sales |
| `calendar.csv` | Date reference — weekday, month, US events, SNAP disbursement flags |
| **Scope** | SKUs: `FOODS_1_001`, `FOODS_1_002`, `FOODS_1_003` · Store: `CA_1` · Jan 29, 2011 → Jan 18, 2012 |

The raw sales file is enormous — 30,490 rows by 1,919 columns. Power Query was used to extract just the three target SKUs without crashing Excel, then INDEX+MATCH joined the sales data to the calendar dimension day by day.

---

## What Each Sheet Does and Why It Matters

### Sheet 1 — RawData
This is the base table everything else references. 355 rows, one per day, with the date, weekday, month, event name, SNAP flag, and daily unit sales for all three SKUs sitting side by side.

It sounds simple, but getting here required pulling three specific rows out of a 30,000-row flat file and reshaping wide sales columns (one column per day) into a vertical time series (one row per day) — which is how analysis tools actually expect time series data to be structured. If this step is sloppy, every analysis downstream inherits the mess.

This sheet is read-only. Nothing gets edited here. Every other sheet pulls from it.

---

### Sheet 2 — SummaryStats
This is where you find out what kind of demand you are actually dealing with.

The key metric here is the **Coefficient of Variation** — standard deviation divided by mean. It tells you how erratic demand is relative to its average level. A CV below 0.2 means demand is stable and predictable. A CV above 0.5 means it is volatile. Above 1.0 means it is genuinely intermittent — the kind of demand where the average is almost meaningless because zero days and spike days are both common.

All three SKUs in this project have a CV above 1.2. Every single one. And when you look at the zero-sales rate, it clicks: more than 50% of all days recorded zero units sold. The median daily sales for all three SKUs is zero.

This matters enormously in practice. A business that looks at average daily sales of 0.90 units and builds a forecast from that number is going to be wrong most days — because most days the real answer is either zero or a small spike, never 0.90. Simple moving averages and basic exponential smoothing were designed for smooth, regular demand. Using them on data like this produces forecasts that are always slightly wrong and never exactly right. The CV analysis in this sheet is what tells you that — before you waste time building the wrong model.

**Concepts: descriptive statistics, demand classification, CV thresholds, intermittent demand identification, outlier detection, IQR and percentile profiling.**

---

### Sheet 3 — WeekdayPattern
The question here is simple: does the day of the week matter?

This sheet calculates average sales per SKU for each day of the week, then converts those averages into a **seasonal index** — a multiplier that shows how each day compares to the weekly average. An index of 1.31 means that day sells 31% above average. An index of 0.72 means it sells 28% below.

The short answer is yes, the day of the week absolutely matters — but not in the same way for every SKU. SKU3 sells 75% above average on Saturdays. SKU1 peaks on Sundays. Monday and Tuesday are consistently weak across all three.

In a real business, this is not just interesting — it is actionable. If your replenishment delivery arrives on Monday and demand spikes on weekends, you need to order earlier or carry enough buffer to cover the gap. If you are staffing a warehouse and you know Friday and Saturday drive the highest pick volumes, you do not schedule your smallest crew those days. The weekday index quantifies something that experienced floor workers often know intuitively but have never seen as a number.

**Concepts: AVERAGEIF for conditional aggregation, seasonal index construction, day-of-week decomposition, application to replenishment timing and labor planning.**

---

### Sheet 4 — MonthlyPattern
Same idea as the weekday analysis, but zoomed out to the full year.

This sheet builds a monthly seasonal index to answer: which months consistently sell above average, and which months are slow? It covers a full 12-month cycle — January 2011 through January 2012 — giving enough data to see the seasonal shape clearly.

The patterns here are more dramatic than the weekday patterns. FOODS_1_001 has a December index of 1.93 and a May index of 1.79 — meaning December sells nearly twice the monthly average. But then between August and October, the same SKU shows near-zero sales. That is not a normal seasonal dip. That is an anomaly. A stockout that was never resolved? A range change that removed the item from the planogram? A data quality issue? The EDA does not answer that question — but it flags it clearly, so whoever builds the forecast in the next project knows not to train a model on those months without investigating first.

That is exactly what EDA is for. Not just to find patterns, but to find the things that look wrong and ask why before they corrupt your analysis.

**Concepts: AVERAGEIF by month, monthly seasonal index, within-year seasonality, anomaly identification, data quality flags for downstream modeling.**

---

### Sheet 5 — EventAnalysis
Retail demand does not exist in a vacuum. People buy differently on Super Bowl Sunday than on a regular Sunday. They shop differently around Thanksgiving. They behave differently during Ramadan, around Easter, around school holidays.

This sheet quantifies exactly how much different.

It calculates average daily sales for each event category — Sporting, Cultural, National, Religious — and compares them to the no-event baseline. The result is an **event lift percentage**: how much sales go up or down relative to a normal day.

The findings here are counterintuitive in places. National holidays — Memorial Day, Independence Day, Labor Day, Thanksgiving — consistently suppress sales across all three SKUs. SKU1 drops 46% on National holiday days. SKU3 drops 43%. This is the opposite of what you might assume if you think "holiday = more shopping." For this category, at this store, people are not stocking up for the holiday — they are not shopping at all.

Sporting events tell a different story. SKU1 and SKU3 jump significantly on sporting event days. SKU2 drops. That kind of split within the same department tells you these items serve different consumption occasions — they are not interchangeable in the customer's mind even though they sit in the same category.

In supply chain practice, this analysis becomes the foundation for **promotional and event-based order adjustments**. If your statistical forecast says you need 10 units the week of Independence Day and your event lift says demand drops 46%, you should be ordering 6 — not 10. Getting that wrong is how holiday overstock accumulates. And overstock in food has a shelf-life problem that overstock in apparel does not.

**Concepts: AVERAGEIF/COUNTIF for event segmentation, lift vs. baseline calculation, external demand driver quantification, event-adjusted ordering logic.**

---

### Sheet 6 — SNAPAnalysis
SNAP is the US government's food assistance program — what was previously called food stamps. Benefits are disbursed on a schedule each month, and for food retailers, those disbursement dates create predictable demand spikes that a model trained only on historical averages will completely miss.

This sheet compares sales on SNAP days vs. non-SNAP days for California (the store is CA_1) and calculates the uplift. SKU2 shows a 14.6% uplift on SNAP days. SKU1 shows 8.8%. SKU3 actually shows a slight negative — which is an interesting signal that these three items serve different customer segments even within the same store.

But the more granular finding is in the secondary analysis: which weekdays are SNAP days in California, and how does sales performance differ when a SNAP day lands on a high-index weekday versus a low one? The combination of a SNAP day on a strong weekday amplifies demand. A SNAP day on a weak weekday partially offsets it. An analyst who only looks at "SNAP vs. non-SNAP" at the month level would miss the interaction entirely.

In real operations, SNAP calendars are published in advance. There is no excuse for a supply chain analyst at a food retailer not to incorporate them into replenishment planning. This sheet shows exactly how to quantify the effect before building it into a planning model.

**Concepts: AVERAGEIF with binary flag, uplift calculation, COUNTIFS/AVERAGEIFS for two-variable interaction, government program demand drivers, demand driver interaction effects.**

---

### Sheet 7 — RollingTrend
Raw daily sales for intermittent items look like noise. A day with 9 units followed by three days of zero followed by a day with 2 units — plotted as a line chart, this tells you almost nothing about where demand is heading.

The rolling average fixes that. This sheet calculates a 28-day (4-week) rolling average and plots it against the actual daily sales. The rolling average absorbs the day-to-day randomness and surfaces the underlying trend.

What it shows for these SKUs is that demand is roughly stationary over the year — no strong growth trend, no clear decline. It oscillates seasonally but does not drift persistently in either direction. That is a useful finding for forecasting: it means you do not need a trend-adjusted model (like Holt-Winters double exponential smoothing). Adding a trend component to a stationary series does not improve accuracy — it adds complexity and potential for error without benefit.

Knowing what your data does not need is just as important as knowing what it does.

**Concepts: rolling window calculations, noise smoothing, trend identification, stationarity assessment, time series chart design.**

---

### Sheet 8 — CorrelationMatrix
The final sheet asks: how related are these three SKUs to each other?

If two items are highly correlated, they respond similarly to the same demand drivers — weekends, events, SNAP days. That validates the patterns found in earlier sheets as category-level behavior, not just quirks of one item. It also has implications for inventory strategy: highly correlated items in the same category can sometimes be managed with shared planning rules rather than fully independent models.

The correlation matrix is paired with a **demand variability ranking** using the CV values from Sheet 2. This gives a clear answer to a practical question: if you had limited time and had to prioritize which SKU to focus your analytical effort on first, which one is most stable (easiest to forecast accurately) and which is most erratic (needs the most safety stock and the most sophisticated approach)?

In a real portfolio of hundreds or thousands of SKUs, this kind of ranking — demand variability segmentation — is how analysts decide where to invest modeling effort and where to use simple rule-based approaches.

**Concepts: Pearson correlation, CORREL function, inter-series relationship analysis, demand variability ranking, SKU prioritization for forecasting and inventory investment.**

---

## Skills Demonstrated

**Data Engineering**
- Power Query: filtering a 30,490-row × 1,919-column flat file to 3 target rows without loading the full dataset
- INDEX+MATCH for horizontal-to-vertical transposition — reshaping wide sales data into a proper time series
- Multi-sheet relational model with a single protected source table feeding all analysis sheets

**Statistical Analysis**
- Full descriptive profile: mean, median, standard deviation, CV, IQR, percentiles, zero-sales rate
- Demand classification using CV thresholds
- Pearson correlation across time series

**Demand Pattern Analysis**
- Weekday and monthly seasonal index construction
- Event type lift quantification vs. no-event baseline
- SNAP uplift analysis with weekday interaction breakdown
- 28-day rolling average for trend isolation and stationarity assessment

**Analytical Thinking**
- Correctly identified all three SKUs as intermittent demand before selecting any modeling approach
- Flagged the August–October anomaly in SKU1 as a data quality / operational issue requiring investigation
- Identified SKU-level behavioral differences within the same department and store
- Connected every finding to a real business or modeling decision — not just reported numbers

---

## Tools

- **Microsoft Excel** — Power Query, INDEX+MATCH, AVERAGEIF / AVERAGEIFS / COUNTIF / COUNTIFS, CORREL, PERCENTILE, STDEV, conditional formatting, charts
- **M5 Forecasting Dataset** — real Walmart retail transaction data, publicly available via Kaggle
- No Python. No Power BI. No third-party add-ins.

---

## Repository