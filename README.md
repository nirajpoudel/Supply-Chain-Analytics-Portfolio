# 🏭 Enterprise Supply Chain Analytics Portfolio
### End-to-End Supply Chain Analytics | M5 Forecasting Dataset

![Supply Chain](https://img.shields.io/badge/Domain-Supply%20Chain%20Analytics-blue)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)
![SQL](https://img.shields.io/badge/SQL-PostgreSQL-336791?logo=postgresql)
![Excel](https://img.shields.io/badge/Excel-Power%20Query-217346?logo=microsoftexcel)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 📌 Overview

This repository contains an end-to-end **Enterprise Supply Chain Analytics Portfolio** built on the [M5 Forecasting Competition dataset (Walmart)](https://www.kaggle.com/competitions/m5-forecasting-accuracy/data) from Kaggle.

The project simulates real-world retail supply chain analytics workflows — starting from foundational Excel-based EDA and scaling progressively through SQL analytics, Python automation, machine learning forecasting, inventory optimization, demand planning, and enterprise-level replenishment systems.

The portfolio is structured to demonstrate skills relevant to roles such as:

> **Supply Chain Analyst · Supply Chain Data Analyst · Inventory Analyst · Demand Planner · Forecasting Analyst · Operations Analyst · BI Analyst · Supply Chain Data Scientist**

---

## 📂 Dataset

**Source:** [Kaggle — M5 Forecasting Accuracy](https://www.kaggle.com/competitions/m5-forecasting-accuracy/data)

| File | Description |
|------|-------------|
| `sales_train_validation.csv` | Daily unit sales per SKU across 10 Walmart stores (5 years) |
| `calendar.csv` | Date features including SNAP events, national/state/cultural holidays |
| `sell_prices.csv` | Weekly sell prices per SKU per store |

**Dataset Scale:**
- 3,049 unique SKUs
- 10 stores across 3 states (CA, TX, WI)
- 3 categories: FOODS, HOBBIES, HOUSEHOLD
- 7 departments
- ~1,941 days of historical sales data

---

## 🗂️ Project Structure
```
supply-chain-analytics/
│
├── data/                               
│   ├── sales_train_validation.csv      
│   ├── calendar.csv                    
│   └── sell_prices.csv                 
│
├── resources/                          
│   ├── notes/                          
│   ├── guides/                         
│   └── links.md                        
│
├── project-0-eda/                      
├── project-1-sales-forecasting/        
├── project-2-inventory-optimization/   
├── project-3-operations-analysis/      
├── project-4-demand-planning/          
├── project-5-replenishment-planning/   
│
├── .gitignore
├── requirements.txt
└── README.md
```
---

## 🚀 Projects

### Project 0 — Exploratory Data Analysis (EDA)
> **Goal:** Understand sales behavior, seasonality, demand variability, event impacts, SKU movement, and product/category/store performance.

**Key Topics:** Sales trend analysis · Demand variability · Seasonality · ABC/XYZ analysis · Fast-moving vs slow-moving inventory · Event/holiday impact · KPI analysis

**Tools:** Excel · Power Query · Pivot Tables · SQL · Python · Tableau / Power BI

**Deliverables:**
- Sales dashboards
- SKU performance analysis
- Store and category analysis reports
- Demand variability reports
- Executive KPI dashboards

---

### Project 1 — Sales Forecasting
> **Goal:** Predict future sales quantity using historical demand patterns and time-series forecasting models across SKU, department, and store levels.

**Forecasting Techniques:**

| Level | Methods |
|-------|---------|
| Beginner | Moving Average, Weighted Average, Exponential Smoothing |
| Intermediate | ARIMA, SARIMA, Prophet |
| Advanced | XGBoost, LightGBM, LSTM |

**Forecast Accuracy Metrics:** MAE · RMSE · MAPE · WAPE

**Tools:** Excel · SQL · Python · Pandas · NumPy · Statsmodels · Prophet · XGBoost · Scikit-learn · Tableau / Power BI

**Deliverables:**
- SKU-level, department-level, and store-level forecasts
- Forecast accuracy dashboards
- Time-series forecasting model pipeline

---

### Project 2 — Inventory Optimization
> **Goal:** Build inventory optimization systems using forecasted demand to determine optimal stock levels, reorder points, safety stock, and inventory risk profiles.

**Key Concepts:** Reorder Point (ROP) · Economic Order Quantity (EOQ) · Safety Stock Optimization · Lead Time Analysis · Service Level Modeling · Stockout Simulation

**Tools:** SQL · Python · Pandas · NumPy · SciPy · Tableau / Power BI

**Deliverables:**
- Inventory optimization dashboard
- Safety stock calculator
- Reorder recommendation engine
- Inventory risk analysis
- Stockout simulation

---

### Project 3 — Supply Chain Operations Analysis
> **Goal:** Analyze operational performance across stores, products, departments, and categories to improve supply chain efficiency.

**KPIs Tracked:**

| KPI | Description |
|-----|-------------|
| Revenue | Total sales revenue by SKU / store / category |
| Units Sold | Volume movement analysis |
| Inventory Turnover | Efficiency of inventory utilization |
| Fill Rate | Order fulfillment efficiency |
| Sell-Through Rate | Inventory liquidation effectiveness |
| Stockout % | Frequency of zero-inventory events |
| Average Selling Price | Pricing trend analysis |

**Tools:** SQL · Python · Tableau / Power BI

**Deliverables:**
- Executive supply chain dashboards
- Store performance dashboards
- SKU performance scorecards
- Category and department analysis reports

---

### Project 4 — Demand Planning
> **Goal:** Build business-driven demand planning systems that incorporate events, promotions, seasonality, and advanced forecasting to generate business-adjusted demand plans.

**Key Topics:** Consensus forecasting · Promotional uplift analysis · Event forecasting · Demand sensing · Scenario planning · Feature engineering · Regression analysis · Time-series ML

**Tools:** Python · Pandas · Scikit-learn · XGBoost · Tableau / Power BI

**Deliverables:**
- Event-based forecasting models
- Promotion uplift models
- Demand planning dashboards
- Scenario simulation reports
- Business-adjusted forecast outputs

---

### Project 5 — Replenishment Planning
> **Goal:** Build replenishment planning systems that translate demand forecasts and inventory policies into actionable replenishment and allocation decisions.

**Key Topics:** Replenishment cycles · Order planning · Allocation planning · Min-max inventory · Service level optimization · Distribution planning · Multi-store replenishment · Inventory simulation

**Tools:** Python · Pandas · NumPy · SciPy · Tableau / Power BI

**Deliverables:**
- Replenishment engine
- Inventory allocation dashboard
- Order recommendation system
- Service-level simulation
- Multi-store replenishment analysis

---

## 📈 Project Scaling Stages

| Stage | Scope | Focus |
|-------|-------|-------|
| **Stage 1 — Excel EDA Sandbox** | CA · CA_1 · HOBBIES · hobbies_1 · 3 SKUs | Excel EDA, Pivot Tables, demand behavior |
| **Stage 2 — SQL Fundamentals** | CA · CA_1 · HOBBIES · hobbies_1 · All SKUs | SQL querying, KPIs, pricing, revenue |
| **Stage 3 — Advanced SQL** | CA · CA_1 · HOBBIES · hobbies_1 + hobbies_2 | Window functions, CTEs, promo analytics |
| **Stage 4 — Python Analytics** | CA · CA_1 · All 3 categories · All departments | Forecasting, inventory optimization, demand planning |
| **Stage 5 — Multi-Store Analytics** | CA · All 4 stores · All categories | Multi-store forecasting, network analysis, inventory balancing |
| **Stage 6 — Enterprise Analytics** | All 3 states · All 10 stores · All SKUs | Enterprise forecasting, hierarchical models, supply chain optimization |

---

## 🛠️ Tech Stack

| Layer | Tools |
|-------|-------|
| **Spreadsheet** | Microsoft Excel, Power Query, Pivot Tables, XLOOKUPs |
| **Database** | PostgreSQL |
| **Programming** | Python 3.10+ |
| **Data Processing** | Pandas, NumPy |
| **Statistics & ML** | Scikit-learn, Statsmodels, SciPy |
| **Forecasting** | Prophet, ARIMA/SARIMA, XGBoost, LightGBM |
| **Deep Learning** | TensorFlow / PyTorch (LSTM) |
| **Visualization** | Matplotlib, Seaborn, Plotly, Tableau / Power BI |
| **Notebook Environment** | Jupyter Notebook / JupyterLab |
| **Version Control** | Git, GitHub |

---

## ⚙️ Setup & Installation

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/supply-chain-analytics.git
cd supply-chain-analytics
```

### 2. Create a Virtual Environment
```bash
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Download the Dataset
Download the M5 Forecasting dataset from Kaggle and place all three files inside the `data/` folder:
```
data/
├── sales_train_validation.csv
├── calendar.csv
└── sell_prices.csv
```

> **Note:** Dataset files are not tracked in this repository due to size. Download them directly from [Kaggle](https://www.kaggle.com/competitions/m5-forecasting-accuracy/data).

---
```
## 📋 Requirements

```
---

## 📊 Business Context

This project simulates the analytics workflows of a **retail supply chain analyst** working with Walmart-scale data. The business questions addressed across all projects include:

- Which SKUs are driving revenue and which are underperforming?
- How do holidays, SNAP events, and promotions impact demand?
- What are the optimal safety stock and reorder points per SKU?
- How accurately can we forecast demand at the SKU/store/category level?
- Which stores face the highest stockout risk?
- How should inventory be allocated across a multi-store network?
- What is the replenishment cycle and order quantity per SKU?

---

## 📁 .gitignore
```
data/
*.csv
*.xlsx
pycache/
.ipynb_checkpoints/
venv/
.env
*.pyc
```
---

## 🗺️ Roadmap

- [x] Project scoping and architecture design
- [ ] Project 0 — Exploratory Data Analysis (EDA)
- [ ] Project 1 — Sales Forecasting
- [ ] Project 2 — Inventory Optimization
- [ ] Project 3 — Supply Chain Operations Analysis
- [ ] Project 4 — Demand Planning
- [ ] Project 5 — Replenishment Planning

---

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## 🙋 About

This portfolio was built to demonstrate enterprise-level supply chain analytics capabilities using real-world retail data. The project is designed to simulate analytical workflows used at large-scale retail and consumer goods organizations.

---

*Built with 📦 supply chain thinking and 🐍 Python.*