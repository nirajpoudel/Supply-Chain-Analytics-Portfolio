# Project 0: Exploratory Data Analysis (EDA) 
## Overview

This project focuses on performing a complete Exploratory Data Analysis (EDA) on retail sales data before any forecasting, inventory planning, or machine learning modeling is attempted.

The objective is to understand the behavior of demand, identify patterns, quantify variability, evaluate the impact of business events, and uncover demand drivers that influence product sales.

This project was completed entirely in Microsoft Excel using structured analytical techniques commonly used by:

- Supply Chain Analysts
- Demand Planners
- Inventory Analysts
- Business Analysts
- Data Analysts
- Forecasting Analysts

Rather than jumping directly into forecasting models, this project follows a business-first approach by understanding the data before making decisions.

---

# Business Problem

Organizations frequently struggle with:

- Unpredictable demand
- Stockouts
- Excess inventory
- Poor forecasting accuracy
- Seasonal demand fluctuations
- Promotional and event-driven demand spikes

Before forecasting future demand, analysts must answer fundamental questions:

- Is demand stable or volatile?
- Which days sell more?
- Which months perform better?
- Do holidays impact sales?
- Does SNAP influence food purchases?
- Are products behaving similarly?
- Are there long-term demand trends?

This project addresses these questions through systematic exploratory analysis.

---

# Dataset Overview

The dataset is derived from the M5 Forecasting Dataset:

### Products Analyzed

- FOODS_1_001
- FOODS_1_002
- FOODS_1_003

### Store

- CA_1 (California)

### Category

- FOODS

### Time Period

- 365 Days
- January 2011 – January 2012

### Additional Business Attributes

- Calendar information
- Weekday information
- Month and year
- Event names
- Event types
- SNAP eligibility days

---

# Project Objectives

The primary objectives were:

✅ Understand demand behavior

✅ Measure demand variability

✅ Identify seasonality patterns

✅ Analyze event impacts

✅ Analyze SNAP impacts

✅ Detect trends over time

✅ Measure product relationships

✅ Build a strong foundation for future forecasting projects

---

# Skills Demonstrated

This project demonstrates practical business analytics skills including:

### Data Preparation

- Data cleaning
- Data transformation
- Data integration
- Data validation

### Excel Analytics

- Pivot-style analysis
- Statistical analysis
- INDEX + MATCH
- XLOOKUPS
- AVERAGEIF
- AVERAGEIFS
- COUNTIFS
- CORREL
- Percentile analysis
- Rolling calculations

### Supply Chain Analytics

- Demand variability analysis
- Seasonal analysis
- Event impact analysis
- Demand driver analysis
- Inventory planning concepts
- Forecasting readiness assessment

---

# Workbook Structure

The workbook contains 8 analytical sheets.

---

# Sheet 1: RawData

## Purpose

This sheet acts as the single source of truth for the entire analysis.

It contains the merged master dataset including:

- Date
- Week information
- Weekday
- Month
- Year
- Event information
- SNAP indicators
- Daily sales for all 3 SKUs

## Business Importance

In real-world organizations, analysts spend significant time creating a clean and trusted dataset before performing analysis.

This sheet represents that foundational data layer from which all subsequent analysis is built.

### Concepts Covered

- Data integration
- Calendar mapping
- Demand history creation
- Master data preparation

---

# Sheet 2: SummaryStats

## Purpose

This sheet builds a statistical profile of each SKU.

Metrics analyzed include:

- Total Units Sold
- Average Daily Sales
- Median Sales
- Standard Deviation
- Coefficient of Variation (CV)
- Maximum Demand
- Minimum Demand
- Zero-Sales Days
- Percentiles
- Interquartile Range (IQR)

## Key Findings

### Demand Variability

| SKU | CV |
|------|------|
| FOODS_1_001 | 1.56 |
| FOODS_1_002 | 1.26 |
| FOODS_1_003 | 1.39 |

All three products exhibit highly variable demand.

A CV greater than 0.50 generally indicates intermittent or difficult-to-predict demand.

### Zero Demand Frequency

More than 50% of days recorded zero sales across all products.

This indicates:

- Intermittent demand
- Forecasting complexity
- Potential inventory planning challenges

## Business Importance

Demand variability directly affects:

- Safety stock calculations
- Reorder points
- Forecast accuracy
- Inventory carrying costs

### Concepts Covered

- Descriptive statistics
- Demand variability
- Forecastability assessment
- Inventory risk indicators

---

# Sheet 3: WeekdayPattern

## Purpose

Analyzes sales behavior by day of the week.

The objective is to determine whether certain weekdays consistently outperform others.

## Business Questions Answered

- Which days generate the highest sales?
- Which days experience weaker demand?
- Should staffing levels vary by weekday?
- Should replenishment schedules change?

## Business Importance

Weekday patterns are critical for:

- Warehouse labor planning
- Replenishment scheduling
- Inventory positioning
- Transportation planning

### Concepts Covered

- Weekly seasonality
- Seasonal index calculation
- Demand pattern recognition
- Workforce planning analytics

---

# Sheet 4: MonthlyPattern

## Purpose

Analyzes sales performance across months.

Monthly averages are used to identify seasonal behavior.

## Business Questions Answered

- Which months perform better?
- Which months experience lower demand?
- Is demand seasonal?

## Business Importance

Monthly seasonality drives:

- Inventory investment decisions
- Capacity planning
- Procurement schedules
- Financial forecasting

### Concepts Covered

- Monthly seasonality
- Seasonal indices
- Time-series decomposition foundations
- Demand planning preparation

---

# Sheet 5: EventAnalysis

## Purpose

Measures how events influence product demand.

Events are categorized as:

- Sporting
- Cultural
- National
- Religious

The analysis compares demand during event periods versus normal periods.

## Business Questions Answered

- Which events increase demand?
- Which events have minimal impact?
- How much demand lift occurs during events?

## Business Importance

Organizations routinely adjust forecasts around:

- Super Bowl
- Christmas
- Thanksgiving
- Valentine's Day
- Other promotional periods

Understanding event impact helps improve forecast accuracy and inventory readiness.

### Concepts Covered

- Demand driver analysis
- Event lift analysis
- Promotional analytics
- Forecast adjustment factors

---

# Sheet 6: SnapAnalysis

## Purpose

Evaluates the impact of SNAP (Supplemental Nutrition Assistance Program) days on food sales.

The analysis compares:

- SNAP Days
- Non-SNAP Days

## Key Findings

### Demand Uplift

| SKU | SNAP Uplift |
|------|------|
| FOODS_1_001 | +8.76% |
| FOODS_1_002 | +14.64% |
| FOODS_1_003 | -8.13% |

The results suggest that SNAP activity influences purchasing behavior differently across products.

## Business Importance

Understanding SNAP impact is important for:

- Grocery retailers
- Demand planners
- Inventory managers
- Store operations teams

It enables organizations to anticipate demand shifts and position inventory appropriately.

### Concepts Covered

- External demand drivers
- Customer purchasing behavior
- Policy-driven demand changes
- Demand segmentation

---

# Sheet 7: Rolling Trend

## Purpose

Identifies long-term demand movement over time.

Metrics include:

- Daily sales
- 28-Day Rolling Average
- 28-Day Rolling Total

## Business Questions Answered

- Is demand growing?
- Is demand declining?
- Is demand stable?

## Business Importance

Trend analysis supports:

- Strategic planning
- Inventory investment decisions
- Forecast model selection
- Product lifecycle analysis

### Concepts Covered

- Moving averages
- Trend detection
- Time-series smoothing
- Demand trajectory analysis

---

# Sheet 8: CorrelationMatrix

## Purpose

Measures relationships between products.

Correlation analysis helps determine whether products respond similarly to demand drivers.

## Key Findings

Observed correlations are relatively weak:

| Relationship | Correlation |
|-------------|-------------|
| SKU1 vs SKU2 | -0.009 |
| SKU1 vs SKU3 | 0.129 |
| SKU2 vs SKU3 | 0.082 |

This suggests that the products do not strongly move together and may require independent forecasting approaches.

## Business Importance

Correlation analysis helps:

- Identify shared demand drivers
- Support product grouping strategies
- Improve forecasting hierarchy design
- Optimize inventory planning

### Concepts Covered

- Correlation analysis
- Product affinity
- Demand relationship modeling
- Forecast segmentation

---

# End-to-End Analytical Approach

This project follows a structured analytical workflow:

### Step 1
Data Collection

↓

### Step 2
Data Cleaning & Integration

↓

### Step 3
Statistical Profiling

↓

### Step 4
Seasonality Analysis

↓

### Step 5
Event Impact Analysis

↓

### Step 6
External Driver Analysis (SNAP)

↓

### Step 7
Trend Detection

↓

### Step 8
Product Relationship Analysis

↓

### Step 9
Forecasting Readiness Assessment

This mirrors the process used by professional analysts before building forecasting models.

---

# What I Learned

Through this project I gained practical experience in:

- Retail demand analysis
- Supply chain analytics
- Data preparation techniques
- Statistical analysis in Excel
- Seasonal demand identification
- Event-driven demand analysis
- Demand variability assessment
- Trend analysis
- Correlation analysis
- Forecasting preparation

Most importantly, I learned that successful forecasting begins with understanding the business and the data rather than immediately applying predictive models.

---

# Project Outcome

By completing this EDA project, I developed a comprehensive understanding of:

- Demand behavior
- Demand variability
- Seasonality
- Event effects
- SNAP effects
- Product relationships
- Long-term trends

These insights provide the analytical foundation required for demand forecasting, inventory planning, and supply chain decision-making.

---

## Portfolio Note

This project is the first stage of a broader Supply Chain Analytics and Floor to Forecasting portfolio roadmap, where each project builds upon the insights and business understanding established during exploratory data analysis.