# HR Workforce Analytics & Attrition Dashboard

**A 4-page Power BI report analyzing workforce trends, attrition drivers, and hiring capacity for a ~1,000-employee organization — built on a custom star-schema data model with 8 fact tables spanning employee lifecycle, compensation, performance, engagement, and recruitment.**

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Data Modeling](https://img.shields.io/badge/Star_Schema-000000?style=for-the-badge)

---

## 📌 Overview

This project analyzes 3 years (Jan 2023–Dec 2025) of workforce data — headcount, hires, exits, engagement, performance, compensation, and recruitment — to answer questions HR and workforce planning teams actually ask: *Where are we losing people, why, and can we hire fast enough to keep up?*

Rather than a single flat dataset, this is built on a proper **star-schema data model** with dedicated fact tables per business process (events, compensation, performance, engagement, absence, recruitment) joined to shared dimensions — the same modeling pattern used in production BI environments, not a one-table "wide CSV" dashboard.

## ❓ Problem

- Leadership needed visibility into **why attrition was elevated (17.1%)** and whether it was concentrated in specific departments, tenure bands, or demographics.
- Recruitment was falling behind demand: **1,576 open requisitions** against only **890 filled**, with no visibility into *which* departments were the bottleneck or *why* (slow time-to-fill vs. low offer-accept).
- Compensation and engagement data existed in separate systems with no single view connecting **pay equity (compa-ratio) → engagement → retention.**

## 🧱 Data Model

Built as a star schema with 4 dimension tables and 8 fact tables (~1,200 employees, ~29K total fact rows):

**Dimensions:** `DimEmployee` · `DimDepartment` · `DimLocation` · `DimDate`

**Facts:**
| Table | Grain | Purpose |
|---|---|---|
| `FactMonthlySnapshot` | Dept × Location × Level × Month | Point-in-time headcount for trend analysis |
| `FactEmployeeEvents` | 1 row per hire/termination event | Drives Hires/Exits KPIs |
| `FactCompensation` | 1 row per salary change | Compa-ratio and pay analysis |
| `FactPerformance` | 1 row per review | Performance rating trends |
| `FactEngagement` | 1 row per survey response | Engagement score trends |
| `FactAbsence` | 1 row per absence event | Absence vs. retention correlation |
| `FactRecruitment` | Dept × Month | Requisition funnel (open/filled/cancelled) |
| `WorkforceTargets` | Dept × Month | Planned headcount & budget vs. actuals |

*<img width="2260" height="765" alt="Data_model" src="https://github.com/user-attachments/assets/cbc7ffb7-5ff9-4dcc-8f8d-1bd1dcc7c6d6" />*

## 📈 Report Pages

### 1. Workforce Overview
Headcount trend (994 current, +59.8% over the period), hires vs. exits, geographic and department distribution, gender split.

### 2. Attrition Analysis
Attrition rate (17.1%), voluntary vs. involuntary split (39.3% / 60.7%), termination reasons, attrition by age band and department, drill-through to individual exit records.

### 3. Retention Drivers
Cross-references engagement (3.6/5), performance (3.4/5), and compa-ratio against retention rate by department and location — surfaces that retention climbs from 79.6% to 88.5% as compa-ratio moves into the 1.00–1.10 band.

### 4. Workforce Planner
Requisition fill rate (56.5%), workforce gap vs. plan (-80, i.e. 92.1% of target), budgeted vs. actual salary cost by department, and a "slow & low-yield" quadrant chart flagging which departments have both long time-to-fill and low fill rates.

## 💡 Key Findings

- **Involuntary exits (60.7%) outweigh voluntary (39.3%)** — the attrition story here is more about performance/restructuring decisions than people leaving voluntarily, which changes the retention strategy conversation.
- **Compa-ratio is a stronger retention lever than engagement alone** — the compa-ratio-to-retention relationship (79.6% → 88.5% retention as pay moves toward market) is clearer than the engagement-to-retention pattern in this dataset.
- **Recruitment, not attrition, is the bigger workforce risk** — with only 56.5% requisition fill rate and a 48-day average time-to-fill, the organization is short 80 heads against plan even before accounting for further attrition.
- **Data & Analytics has the longest hiring cycle (56 days)** — worth flagging as its own bottleneck rather than assuming all departments hire at the same speed.

## 🧰 Tech Stack

| Layer | Tool |
|---|---|
| Data Modeling | Power BI (star schema, 4 dims + 8 facts) |
| Transformation | Power Query |
| Metrics | DAX |
| Visualization | Power BI (custom Chiclet Slicer, drill-through, bookmarks) |

<!--
## 🔗 Live Report

*(Recommended: publish to Power BI Service and link here, or publish to Power BI Public if the dataset stays fully synthetic — a clickable live report is significantly more convincing to reviewers than static screenshots.)*

---
-->
