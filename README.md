# Customer Segmentation using RFM Analysis
### Power BI · AdventureWorks Dataset · 18,484 Customers · $29.36M Revenue

> Segment customers by purchasing behaviour, identify churn risks, and deliver targeted marketing recommendations — all powered by RFM (Recency, Frequency, Monetary) analysis.

---

## Project Overview

This project performs end-to-end RFM-based customer segmentation on the AdventureWorks transactional dataset. Customers are scored across three dimensions and grouped into 11 behaviour-driven segments. The output is an interactive Power BI dashboard with demographic breakdowns, geographic sales mapping, and per-segment RFM diagnostics.

---

## Repository Structure

```
Customer-Segmentation-RFM/
├── Customer_Analytics.pbix      # Power BI report (all visuals & DAX)
├── data/
│   └── AdventureWorksDW.xlsx    # Source transactional data
└── README.md
```

---

## Methodology

### Step 1 — Data Cleaning & Preparation
- Loaded `FactInternetSales`, `DimCustomer`, `DimProduct`, and `DimDate` tables
- Removed nulls, standardised date formats, and resolved duplicate `CustomerKey` entries
- Merged customer demographic attributes (age, gender, marital status, country)

### Step 2 — RFM Metric Calculation

| Metric | Definition | Formula |
|--------|-----------|---------|
| Recency (R) | Days since last purchase | `Snapshot Date - Max(OrderDate)` |
| Frequency (F) | Number of distinct orders | `COUNT(DISTINCT SalesOrderNumber)` |
| Monetary (M) | Total revenue generated | `SUM(SalesAmount)` |

Each metric is scored 1-5 using quintile binning (5 = best). Scores are summed to produce an RFM Score (3-15).

### Step 3 — Customer Segmentation

Customers are assigned to one of 11 segments based on R/F/M score combinations:

| Segment | R | F | M | Description |
|---------|---|---|---|-------------|
| Champions | 5 | 5 | 5 | Bought recently, buy often, spend the most |
| Loyal Customers | >=4 | >=3 | >=3 | Regular buyers with solid spend |
| New Customers | 5 | 1 | 1 | Recent first-time buyers |
| Promising | 4 | 1-2 | 1-2 | Recent but infrequent — high potential |
| At Risk | 2-3 | >=3 | >=3 | Once loyal, now drifting away |
| Hibernating | 2 | 2 | 2 | Low recency, frequency, and spend |
| About To Sleep | 2 | 1 | 1 | Very inactive, may be lost soon |
| Lost Customers | 1 | 1-2 | 1-2 | Haven't purchased in a long time |
| Cannot Lose Them | 1 | 5 | 5 | High-value but haven't returned |
| Potential Loyalists | 3 | 1 | 1 | Bought more than once, moderate recency |
| Need Attention | 3 | 2 | 2 | Above-average but showing decline |

### Step 4 — Behaviour Analysis

- **Demographics**: Sales broken down by age band (55-64 highest), marital status (51.7% married), and gender (near 50/50 split)
- **Geography**: Bubble map reveals North America and Australia as primary revenue markets
- **RFM Patterns**: Champions and At Risk customers dominate Frequency and Monetary totals — opposing ends of the loyalty spectrum

### Step 5 — Marketing Recommendations

| Segment | Strategy |
|---------|----------|
| Champions | Reward with loyalty perks, early product access, referral incentives |
| At Risk | Re-engage via win-back campaigns and personalised discounts |
| Cannot Lose Them | High-urgency outreach — direct contact, exclusive offers |
| New Customers | Welcome series, onboarding emails, first-purchase follow-ups |
| Promising | Targeted upsell nudges to build purchase frequency |
| Hibernating | Low-cost reactivation; survey to understand drop-off |
| Lost Customers | Minimal spend; sunset or last-chance reactivation only |

### Step 6 — Visualisation (Power BI)

- Donut charts — Marital status and gender split
- Horizontal bar charts — Sales by age band and customer count by segment
- Bubble map — Total sales by country
- 3-panel RFM bar charts — Recency, Frequency, Monetary totals per segment
- Detail table — Individual customer records with full RFM attributes

---

## Key Findings

| Insight | Value |
|---------|-------|
| Total Customers | 18,484 |
| Total Revenue | $29.36M |
| Highest-value age group | 55-64 |
| Largest segment | New Customers |
| Highest avg spend/customer | Champions ($4,439) |
| Biggest re-engagement opportunity | At Risk (23% of base, ~$10.2M) |

---

- **Power BI Desktop** — data modelling, DAX measures, interactive visuals
- **Power Query (M)** — data cleaning and transformation
- **DAX** — RFM scoring, segment logic, KPI calculations
- **AdventureWorks DW** — source OLAP dataset (Microsoft sample)

---

*Project completed as part of the SyntecxHub Power BI training programme.*
