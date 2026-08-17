
# Supply Chain & Shipment Performance Analytics

An end-to-end Supply Chain Analytics project that analyzes shipment performance, identifies delivery delay patterns, validates data quality, and provides operational insights through an interactive Power BI dashboard.

---

## Project Overview

Delivery performance is an important part of supply chain and logistics operations. Delays can vary across delivery partners, regions, weather conditions, vehicle types, delivery modes, distance, and package weight.

This project analyzes **25K+ shipment records** to monitor delivery performance, identify high-delay segments, evaluate delay severity, and detect data quality exceptions.

The solution follows a Control Tower-oriented analytical workflow:

> **Monitor → Identify → Analyze → Investigate → Follow Up**

---

# Business Objective

The project aims to build an operational analytics solution that helps:

- Monitor overall shipment and delivery performance
- Measure On-Time Delivery and Delay Rates
- Identify operational dimensions with higher delay exposure
- Analyze delay duration and severity
- Detect data quality and reporting inconsistencies
- Drill down to shipment-level exceptions for operational follow-up

---

# Business Questions

The analysis addresses the following business questions:

1. What is the overall delivery performance?
2. What percentage of shipments are delivered on time versus delayed?
3. Which regions and operational dimensions have higher delay rates?
4. How severe are the delivery delays?
5. Does delivery distance or package weight show different delay patterns?
6. Which shipment records contain data quality issues?
7. Which operational segments should be prioritized for further investigation?
8. Which individual shipments require operational follow-up?

---

# Dataset

**Dataset Size:** 25K+ shipment records

The dataset contains shipment, transportation, operational, delivery-time, and cost information.

| Category | Fields |
|---|---|
| Shipment | `delivery_id`, `delivery_status` |
| Delivery Partner | `delivery_partner` |
| Package | `package_type`, `package_weight_kg` |
| Transportation | `vehicle_type`, `delivery_mode` |
| Location | `region` |
| External Conditions | `weather_condition` |
| Distance | `distance_km` |
| Delivery Time | `delivery_time_hours`, `expected_time_hours` |
| Delay | `delayed` |
| Customer Feedback | `delivery_rating` |
| Cost | `delivery_cost` |

---

# Tools & Technologies

- **Python** – Data cleaning, validation, preprocessing
- **Google Colab** – Data processing and analysis
- **MySQL** – Data querying and analytical preparation
- **Power BI** – Dashboard development and visualization
- **DAX** – KPI calculations and analytical business logic

---

# Project Workflow

```text
Raw Shipment Data
        │
        ▼
Data Profiling
        │
        ▼
Data Cleaning & Validation
        │
        ├── Duplicate Detection
        ├── Time Data Validation
        ├── Data Standardization
        └── Data Quality Checks
        │
        ▼
Clean Shipment Dataset
        │
        ▼
Power BI Data Model
        │
        ├── DAX KPI Development
        ├── Delay Classification
        ├── Delay Reconciliation
        └── Dynamic Dimension Analysis
        │
        ▼
Interactive Power BI Dashboard
        │
        ├── Performance Monitoring
        ├── Delay Analysis
        ├── Operational Dimension Analysis
        └── Shipment-level Investigation
        │
        ▼
Business Insights
        │
        ▼
Operational Follow-up
````

---

# 1. Data Preparation & Validation

The raw shipment dataset was processed and validated before being loaded into Power BI.

### Data preparation activities

* Inspected dataset structure and data types
* Checked missing and invalid values
* Standardized categorical fields
* Validated delivery-time fields
* Identified duplicate delivery IDs
* Prepared distance and weight groups
* Validated shipment status and delay-related fields

Actual delivery time was compared with expected delivery time to independently assess delivery performance.

```text
Delay Duration
= Actual Delivery Time - Expected Delivery Time
```

This calculated result was later used for delay analysis and reconciliation against the reported `delayed` field.

---

# 2. Data Quality & Reconciliation

Data quality was incorporated into the reporting workflow to improve the reliability of operational KPIs.

## Duplicate Delivery ID

Identifies shipment records where the same `delivery_id` appears multiple times.

## Time Data Validation

Checks whether actual and expected delivery-time values are valid and suitable for delay calculations.

## Delay Reconciliation

The reported `delayed` status is compared with the independently calculated delivery performance.

```text
Actual Time > Expected Time
        ↓
Calculated Delay = Yes

Actual Time ≤ Expected Time
        ↓
Calculated Delay = No
```

Records where the reported status does not match the calculated result are flagged as reconciliation exceptions.

### Data Quality Exceptions

The dashboard consolidates:

* Duplicate delivery IDs
* Invalid time records
* Delay reconciliation mismatches

Approximately **2K records** were identified as data quality exceptions requiring further validation or follow-up.

---

# 3. KPI Development

The main operational KPIs were calculated using DAX in Power BI.

### Core KPIs

| KPI                     |         Result |
| ----------------------- | -------------: |
| Total Deliveries        |       **25K+** |
| On-Time Delivery Rate   |      **73.3%** |
| Delay Rate              |      **26.7%** |
| Average Delay           | **2.94 hours** |
| Total Delivery Cost     |     **21.62M** |
| Data Quality Exceptions |        **~2K** |

These KPIs provide the overall performance baseline before moving into dimension-level analysis.

---

# 4. Delay Severity Analysis

Delayed shipments were classified into five severity levels:

| Delay Severity      | Purpose                              |
| ------------------- | ------------------------------------ |
| **On Time / Early** | Delivered on or before expected time |
| **Minor Delay**     | Short delivery delay                 |
| **Moderate Delay**  | Medium delivery delay                |
| **Severe Delay**    | Significant delivery delay           |
| **Critical Delay**  | Extreme delivery delay               |

The severity classification allows the dashboard to distinguish between:

> **How often delays happen**

and

> **How severe those delays are**

---

# 5. Power BI Dashboard

The final solution contains **two interactive dashboard pages**.

---

## Page 1 — Supply Chain & Shipment Performance Analytics

The first page provides an overall view of shipment performance.

### Main KPIs

* Total Deliveries
* On-Time Delivery Rate
* Delay Rate
* Average Delay Hours
* Total Delivery Cost
* Data Quality Exceptions

### Main Visuals

**On-Time Delivery Performance by Dimension**

Provides dynamic comparison of delivery performance across different operational dimensions.

**Delivery Volume & Delay Performance**

Compares shipment volume and Delay Rate across the selected dimension.

### Dynamic Dimensions

Users can switch between:

* Delivery Partner
* Region
* Weather Condition
* Vehicle Type
* Delivery Mode
* Distance Group
* Weight Group

This allows multiple operational analyses without creating separate visuals for every dimension.

---

# Page 2 — Delay & Root Cause Analysis

The second page focuses on identifying and investigating delivery delay patterns.

### Main Visuals

**Delay Rate & Average Delay Hours by Performance Dimension**

Compares both the frequency and duration of delays.

**Shipment Distribution by Delay Severity**

Shows how shipments are distributed across On Time / Early, Minor, Moderate, Severe, and Critical Delay categories.

**Delay Performance by Distance / Weight**

Analyzes delay patterns across distance and package-weight groups.

**Shipment-level Exception Table**

Provides detailed records for operational investigation, including:

* Delivery ID
* Region
* Distance
* Delay Status
* Delay Severity
* Delivery Partner
* Shipment Status

---

# 💡 Key Insights

## Insight 1 — Overall Delivery Reliability

The dataset contains **25K+ deliveries**, with:

* **73.3% On-Time Delivery Rate**
* **26.7% Delay Rate**
* **2.94 hours Average Delay**

This means that approximately **1 in every 4 shipments experienced a delay**.

The overall Delay Rate indicates that delivery reliability is a meaningful operational area for further investigation.

---

## Insight 2 — Regional Performance Is Relatively Consistent

Regional Delay Rates are relatively close:

| Region  | Delay Rate |   Avg. Delay |
| ------- | ---------: | -----------: |
| Central | **27.27%** | **2.92 hrs** |
| West    | **27.05%** | **2.96 hrs** |
| South   | **26.89%** | **2.99 hrs** |
| North   | **26.59%** | **2.85 hrs** |
| East    | **25.80%** | **2.96 hrs** |

### Interpretation

**Central** has the highest Delay Rate at **27.27%**, while **East** has the lowest at **25.80%**.

However, the gap between the highest and lowest regions is only about **1.47 percentage points**.

This suggests that:

> **Region alone does not explain the overall delivery delay pattern.**

Further analysis across partner, weather, vehicle, delivery mode, distance, and package weight is therefore required.

---

## Insight 3 — Delay Frequency Is More Important Than Extreme Delay Severity

The shipment distribution shows approximately:

* **19.1K On Time / Early**
* **2.6K Minor Delay**
* **2.2K Moderate Delay**
* **0.5K Severe Delay**
* **~0K Critical Delay**

### Interpretation

Most delayed shipments fall into the **Minor** or **Moderate Delay** categories.

Severe delays represent a much smaller proportion, while Critical Delay cases are negligible.

This indicates that the operational challenge is primarily:

> **Reducing the frequency of regular delivery delays rather than managing a large number of extreme delays.**

---

## Insight 4 — Delay Rate and Average Delay Tell Different Stories

The dashboard compares both **Delay Rate** and **Average Delay Hours**.

For example:

* **Central** has the highest Delay Rate: **27.27%**
* **South** has the highest Average Delay: approximately **2.99 hours**
* **North** has the lowest Average Delay: approximately **2.85 hours**

### Interpretation

The region with the highest number of delayed shipments is not necessarily the region with the longest delays.

Therefore, operational monitoring should consider both:

> **Delay Frequency + Delay Duration**

rather than relying on Delay Rate alone.

---

## Insight 5 — Long-Distance Shipments Show Higher Delay Exposure

The **50+ km distance group** consistently shows higher Delay Rates across package-weight categories.

For example:

| Weight Group | Delay Rate for 50+ km |
| ------------ | --------------------: |
| Heavy        |            **28.91%** |
| Light        |            **28.64%** |
| Medium       |            **28.35%** |

### Interpretation

The 50+ km segment shows a consistently higher delay rate than shorter-distance segments.

This makes long-distance shipments a useful priority segment for further investigation, particularly around:

* Route planning
* Transit-time assumptions
* Delivery scheduling
* Carrier allocation
* Long-distance operational constraints

> **Important:** This is an observed pattern in the dataset, not proof that distance is a causal driver of delays.

---

## Insight 6 — Package Weight Does Not Appear to Be the Primary Differentiator

Within the 50+ km distance group, Delay Rates remain relatively high across:

* Light packages
* Medium packages
* Heavy packages

The differences between weight groups are relatively small compared with the difference associated with the long-distance segment.

### Interpretation

This suggests that **distance may warrant more attention than package weight** when prioritizing the next stage of operational investigation.

However, further statistical analysis would be required before making any causal conclusion.

---

## Insight 7 — Operational Performance Requires Multi-Dimensional Analysis

The dashboard allows performance to be analyzed across seven dimensions:

> **Delivery Partner → Region → Weather → Vehicle Type → Delivery Mode → Distance → Weight**

This is important because no single dimension explains the entire delay pattern.

For example, a segment may have:

* A high Delay Rate but low Average Delay
* A moderate Delay Rate but high Average Delay
* A high shipment volume but average delivery performance
* A low volume but disproportionately high delay exposure

The dashboard therefore supports **segment-level prioritization rather than one-dimensional reporting**.

---

## Insight 8 — Data Quality Is a Reporting Risk

Approximately **2K records** were flagged as data quality exceptions.

These exceptions were detected through:

* Duplicate Delivery ID checks
* Invalid time-data checks
* Delay reconciliation

### Interpretation

Data quality issues can directly affect operational KPIs.

For example, inconsistent actual or expected delivery times can affect:

* Delay Rate
* Average Delay
* Delay Severity
* On-Time Delivery Rate

Therefore:

> **Data quality validation should be treated as part of the operational reporting process, not as a separate technical activity.**

---

## Insight 9 — Shipment-Level Investigation Connects Analytics to Operations

The second dashboard page allows users to move from aggregated analysis to individual shipment records.

For example:

```text
High Delay Rate Segment
        ↓
Identify Region / Partner / Distance
        ↓
Analyze Delay Severity
        ↓
Filter Priority Segment
        ↓
Review Individual Delivery IDs
        ↓
Operational Investigation
```

This enables the dashboard to support not only reporting but also **exception management and operational follow-up**.

---

# 📖 Dashboard Storytelling

The dashboard is designed around a simple operational storytelling framework:

### 1. What happened?

The first page establishes the overall delivery performance:

> **73.3% On-Time Delivery vs. 26.7% Delay Rate**

### 2. Where is the issue?

The dashboard compares performance across:

> Partner → Region → Weather → Vehicle → Mode → Distance → Weight

### 3. How serious is the issue?

Delay Severity shows that most delays are **Minor or Moderate**, while Severe and Critical cases represent a much smaller proportion.

### 4. What patterns should be investigated?

The analysis highlights:

* Higher delay exposure in the **50+ km** segment
* Differences between Delay Rate and Average Delay across regions
* Operational variation across partners and other dimensions

### 5. Which records require follow-up?

The shipment-level table allows users to drill down into specific delivery records and investigate operational exceptions.

---

# 🎯 Business Value

The project transforms raw shipment data into a structured operational analytics solution.

It supports three levels of decision-making:

| Analytical Level  | Business Question                    | Dashboard Output                                          |
| ----------------- | ------------------------------------ | --------------------------------------------------------- |
| **Monitoring**    | How is overall delivery performance? | OTD, Delay Rate, Volume, Cost                             |
| **Diagnosis**     | Where are delays concentrated?       | Partner, Region, Weather, Vehicle, Mode, Distance, Weight |
| **Investigation** | Which shipments require follow-up?   | Delay Severity & Shipment-level Exceptions                |

The solution connects:

> **Performance Monitoring → Data Quality → Delay Analysis → Segment Prioritization → Shipment Investigation**

---

# 🚀 Key Takeaways

The project demonstrates an end-to-end approach to operational analytics:

```text
Data Preparation
      ↓
Data Quality Validation
      ↓
KPI Development
      ↓
Power BI Dashboard
      ↓
Multi-Dimensional Analysis
      ↓
Delay & Severity Analysis
      ↓
Exception Investigation
```

The main analytical takeaway is that **delivery performance should not be evaluated using a single KPI**.

Combining:

* On-Time Delivery Rate
* Delay Rate
* Average Delay Hours
* Delay Severity
* Shipment Volume
* Operational Dimensions
* Data Quality Exceptions

provides a more complete view of supply chain performance and helps identify where operational teams should focus further investigation.

---

# Project Structure

```text
Supply-Chain-Shipment-Performance-Analytics/
│
├── data/
│   ├── raw/
│   │   └── Delivery_Logistics.csv
│   │
│   └── processed/
│       └── Delivery_logistics_clean.csv
│
├── notebooks/
│   └── shipment_data_preparation.ipynb
│
├── powerbi/
│   └── Delivery.pbix
│
└── README.md
```

---

# Dashboard Preview

## Page 1 — Supply Chain & Shipment Performance Analytics

---

## Page 2 — Delay & Root Cause Analysis

---

# 🧠 Skills Demonstrated

### Data Analytics

* Data Cleaning
* Data Validation
* Data Reconciliation
* Exploratory Data Analysis
* Operational Analysis
* Segment Analysis
* Exception Analysis

### Business Intelligence

* Power BI
* DAX
* KPI Development
* Interactive Dashboard Design
* Field Parameters
* Dynamic Dimension Analysis
* Drill-down Analysis

### Data & Database

* Python
* Data Quality Controls

### Supply Chain & Logistics

* Shipment Performance
* Delivery Operations
* Logistics Analytics
* Operational Excellence
* Control Tower Analytics
* Exception Management

---

# 📚 Dataset Source

The dataset is used for educational and portfolio purposes.

> No confidential or proprietary business data is included in this project.


