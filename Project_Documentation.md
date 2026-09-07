# 🚚 Supply Chain Control Tower — Power BI Analytics Project

## 1. Project Overview

The **Supply Chain Control Tower** is an interactive Power BI analytics solution designed to provide a consolidated view of supply chain performance, supplier risk, logistics efficiency, warehouse conditions, and operational disruptions.

The dashboard transforms raw supply chain data into actionable business intelligence through **Power Query, data modeling, DAX measures, interactive visualizations, drill-through analysis, and management-level recommendations**.

The solution follows a structured analytical flow:

**Raw Data → Data Cleaning → Data Modeling → DAX Analysis → Dashboard → Business Insights → Recommendations**

---

## 2. Business Problem

Modern supply chains face multiple interconnected risks, including:

* Supplier reliability issues
* Delivery delays
* Transportation cost fluctuations
* Inventory imbalance
* Operational disruptions
* Route and weather-related risks
* Customs clearance delays
* Cargo condition issues

Without a centralized analytical view, it can be difficult for decision-makers to identify high-risk areas and prioritize corrective actions.

This project addresses the problem by providing a **centralized Supply Chain Control Tower** that enables users to monitor performance and investigate potential risk drivers.

---

## 3. Project Objectives

The primary objectives of this project are to:

* Monitor overall supply chain performance
* Identify high-risk suppliers and risk exposure
* Analyze supplier reliability and delivery risk
* Evaluate logistics costs and lead times
* Analyze inventory and warehouse operational indicators
* Investigate disruption and delivery risk drivers
* Compare risk patterns across countries
* Provide actionable business recommendations
* Enable interactive filtering and supplier-level investigation

---

## 4. Dataset

The project uses a dynamic supply chain logistics dataset containing operational, supplier, logistics, risk, inventory, and country-level information.

### Dataset Characteristics

* **18 columns**
* Approximately **113K records**
* Supplier-level and product-level information
* Country-level information
* Operational risk indicators
* Logistics performance metrics

### Key Fields

| Category         | Fields                                                                                        |
| ---------------- | --------------------------------------------------------------------------------------------- |
| Inventory        | `warehouse_inventory_level`, `historical_demand`                                              |
| Warehouse        | `handling_equipment_availability`                                                             |
| Logistics        | `shipping_costs`, `lead_time_days`, `delivery_time_deviation`                                 |
| Supplier         | `supplier_id`, `supplier_reliability_score`                                                   |
| Risk             | `risk_classification`, `route_risk_level`, `disruption_likelihood_score`, `delay_probability` |
| Operations       | `order_fulfillment_status`, `cargo_condition_status`                                          |
| External Factors | `weather_condition_severity`, `customs_clearance_time`                                        |
| Product          | `product_id`                                                                                  |
| Geography        | `supplier_country`                                                                            |

---

# 5. Data Preparation — Power Query

The raw dataset was processed using **Power Query** before being loaded into the analytical model.

### Data Quality Checks

The following checks were performed:

* Missing value validation
* Error validation
* Duplicate record validation
* Data type verification
* Category/value inspection
* Column-level profiling

### Results

* **Missing values:** 0%
* **Errors:** 0%
* **Complete duplicate rows:** None identified
* Data types were reviewed and corrected where required.
* Categorical fields were validated.
* Repeated Product IDs were identified and treated appropriately during modeling.

The objective of this stage was to ensure that the dataset was reliable and suitable for analytical modeling.

---

# 6. Data Modeling

The project uses a **Star Schema** to create a structured and scalable analytical model.

### Fact Table

**`Fact_SupplyChain`**

Contains the main operational and transactional-level supply chain records.

### Dimension Tables

**`Dim_Product`**

* `product_id`

**`Dim_Supplier`**

* `supplier_id`

**`Dim_Country`**

* `supplier_country`

### Relationships

The following one-to-many relationships were established:

```text
Dim_Product
     │
     │ 1 : *
     ▼
Fact_SupplyChain

Dim_Supplier
     │
     │ 1 : *
     ▼
Fact_SupplyChain

Dim_Country
     │
     │ 1 : *
     ▼
Fact_SupplyChain
```

Relationships use:

* **Cardinality:** One-to-Many
* **Cross-filter direction:** Single

A separate Date table was not required because the source dataset does not contain a date field.

---

# 7. DAX Measures

A total of **20 DAX measures** were developed to support KPI calculations and dashboard analysis.

### Core KPIs

* Total Records
* Total Shipping Cost
* Average Lead Time
* Average Risk Score
* Average Delay Probability
* Average Delivery Deviation
* Average Disruption Likelihood
* Total Historical Demand
* Average Inventory Level
* Average Equipment Availability

### Risk Analysis

* High-Risk Records
* High-Risk %
* Low-Risk Records
* Moderate-Risk Records

### Operational Metrics

* Average Customs Clearance Time
* Average Shipping Cost
* Average Supplier Reliability
* Average Route Risk
* Average Weather Severity
* Average Cargo Condition

These measures were formatted appropriately as **whole numbers, decimals, and percentages** depending on their business meaning.

---

# 8. Dashboard Architecture

The dashboard is organized into six primary analytical pages, supported by a supplier-level drill-through page.

### Analytical Flow

```text
Executive Control Tower
          ↓
Supplier Risk Analysis
          ↓
Logistics & Delivery
          ↓
Warehouse & Inventory
          ↓
Risk Investigation
          ↓
Business Insights & Recommendations
```

### Supporting Detail Page

**Supplier Detail**

The Supplier Detail page provides a deeper supplier-level view through drill-through functionality.

---

# 9. Dashboard Pages

## 9.1 Executive Control Tower

### Purpose

Provides a high-level management view of supply chain performance and risk exposure.

### Key KPIs

* Total Records
* Total Shipping Cost
* Average Lead Time
* Average Delay Probability
* High-Risk %

### Key Visuals

* Risk Distribution
* Delay Probability by Risk
* Top Supplier Reliability
* Delay Probability by Country
* Average Shipping Cost by Risk

### Business Question

**“What is the current overall supply chain risk and performance position?”**

---

## 9.2 Supplier Risk Analysis

### Purpose

Analyzes supplier reliability, risk exposure, disruption risk, and delivery performance.

### Key KPIs

* Average Supplier Reliability
* High-Risk Records
* High-Risk %

### Key Visuals

* Top Supplier Reliability
* Supplier Reliability vs Delay Risk
* Supplier Risk Exposure
* Supplier Reliability vs Disruption Risk

### Business Question

**“Which suppliers require attention, and how does supplier reliability relate to operational risk?”**

### Key Insight

Supplier risk levels do not necessarily translate directly into higher delay probability, highlighting the importance of evaluating supplier reliability and operational risk independently.

---

## 9.3 Logistics & Delivery

### Purpose

Evaluates transportation costs, lead times, delivery risk, and fulfillment performance.

### Key KPIs

* Total Shipping Cost
* Average Shipping Cost
* Average Lead Time
* Average Delay Probability

### Key Visuals

* Shipping Cost by Country
* Lead Time vs Delay Risk
* Shipping Cost by Risk Level
* Order Fulfillment by Risk Level

### Business Question

**“Where are logistics costs and delivery risks concentrated?”**

### Key Insight

Shipping costs vary across countries, while risk levels show differences in logistics cost and delivery performance, indicating opportunities to optimize transportation and manage delivery risk.

---

## 9.4 Warehouse & Inventory

### Purpose

Evaluates inventory health, demand, warehouse readiness, and operational conditions.

### Key KPIs

* Average Inventory Level
* Total Historical Demand
* Average Equipment Availability
* Average Cargo Condition

### Key Visuals

* Inventory vs Demand
* Equipment Availability by Country
* Inventory by Risk Level

### Business Question

**“Are warehouse and inventory indicators aligned with supply chain risk?”**

### Key Insight

Despite high overall risk exposure, cargo condition, customs clearance time, and weather severity show relatively limited variation across risk levels, suggesting that these factors are not the primary drivers of the observed risk.

---

## 9.5 Risk Investigation

### Purpose

Performs root-cause-oriented analysis of disruption and delivery risk.

### Key KPIs

* Average Risk Score
* Average Disruption Likelihood
* Average Delay Probability
* High-Risk %

### Key Visuals

* Risk Classification
* Disruption vs Delay
* Route Risk
* Weather Severity vs Delay Risk
* Cargo Condition vs Delay Risk
* Customs Clearance vs Delay Risk

### Business Question

**“What operational factors are associated with supply chain risk and delivery exposure?”**

---

## 9.6 Business Insights & Recommendations

### Purpose

Provides the final management-level interpretation of the analysis.

This page consolidates the key findings from the analytical pages and converts them into actionable business recommendations.

### Overall Business Takeaway

The analysis highlights significant supply chain risk exposure, with supplier and operational risks requiring the greatest attention. While logistics costs and delivery performance vary across suppliers and countries, cargo condition, customs clearance, and weather show limited variation across risk levels.

This indicates an opportunity to prioritize supplier risk management, strengthen operational monitoring, and focus mitigation efforts on the factors with the greatest business impact.

### Recommended Management Actions

**Prioritize high-risk suppliers → Strengthen monitoring → Optimize logistics → Reduce disruption and delivery exposure**

---

# 10. Interactive Features

The dashboard was designed with an interactive analytical experience.

### Slicers

Users can filter the dashboard by:

* Supplier Country
* Risk Classification
* Supplier ID

### Page Navigation

A page navigator enables users to move between the major analytical sections.

### Drill-through

The **Supplier Detail** page enables deeper supplier-level investigation.

### Cross-Filtering

Visuals interact dynamically when users select categories, suppliers, countries, or risk levels.

This allows users to move from **high-level monitoring to detailed investigation** without leaving the Power BI report.

---

# 11. Business Storytelling

The dashboard follows a management-oriented analytical storyline:

### 01 — Monitor

**Executive Control Tower**

Understand the overall supply chain position.

### 02 — Identify

**Supplier Risk Analysis**

Identify supplier reliability and risk exposure.

### 03 — Optimize

**Logistics & Delivery**

Investigate transportation cost and delivery performance.

### 04 — Assess

**Warehouse & Inventory**

Evaluate inventory and warehouse operational indicators.

### 05 — Investigate

**Risk Investigation**

Explore potential risk drivers and operational relationships.

### 06 — Act

**Business Insights & Recommendations**

Convert analytical findings into business actions.

---

# 12. Key Business Recommendations

Based on the analysis, organizations can consider the following actions:

### Supplier Risk Management

* Prioritize monitoring of high-risk suppliers.
* Review supplier reliability regularly.
* Develop supplier-specific mitigation strategies.
* Consider diversification for critical supplier dependencies.

### Logistics Optimization

* Investigate countries with comparatively higher shipping costs.
* Monitor suppliers with elevated delivery risk.
* Identify opportunities to optimize transportation routes and costs.

### Operational Monitoring

* Track disruption likelihood and delay probability continuously.
* Monitor route risk and fulfillment performance.
* Establish early-warning indicators for high-risk conditions.

### Warehouse & Inventory

* Monitor inventory against historical demand.
* Maintain adequate warehouse equipment availability.
* Investigate inventory patterns associated with elevated risk.

---

# 13. Technology Stack

### Data & Analytics

* **Power BI**
* **Power Query**
* **DAX**
* **Microsoft Excel / CSV**

### Analytical Techniques

* Data cleaning
* Data profiling
* Data modeling
* Star schema
* KPI development
* Risk analysis
* Supplier analysis
* Logistics analysis
* Interactive dashboarding
* Business storytelling

---

# 14. Skills Demonstrated

This project demonstrates practical capabilities in:

**Power BI | DAX | Power Query | Data Modeling | Data Cleaning | KPI Development | Risk Analytics | Supply Chain Analytics | Business Intelligence | Data Visualization | Dashboard Design | Business Storytelling**

---

# 15. Project Outcome

The Supply Chain Control Tower converts a large operational dataset into an interactive analytical solution that enables users to:

* Monitor supply chain performance
* Identify risk exposure
* Analyze supplier performance
* Evaluate logistics efficiency
* Investigate operational risk factors
* Compare performance across countries
* Drill into supplier-level details
* Translate data into business recommendations

The project demonstrates an end-to-end **Data Analytics → Business Intelligence → Decision Support** workflow using Power BI.

---

## 16. Portfolio Value

This project showcases the ability to move beyond simply creating charts and instead build a **business-focused analytical product**.

It demonstrates the complete workflow:

**Raw Data → Data Quality → Data Model → DAX → Visualization → Interactive Analysis → Business Insights → Recommendations**

The final solution is designed as a **Supply Chain Control Tower**, providing management with a structured view of operational performance and risk.
