# 🚚 Supply Chain Control Tower — Power BI Report

An end-to-end **Power BI** dashboard that turns raw supply chain, supplier, logistics, and warehouse data into a single control tower for tracking risk, cost, and delivery performance — and for tracing *why* disruptions are happening.

The report follows a deliberate analytical narrative across seven pages:

> **Performance overview → Risk identification → Root-cause investigation → Recommendations**

---

## 📁 File

| File | Description |
|---|---|
| `Supply_Chain_control_tower.pbix` | Power BI Desktop file — full data model, DAX measures, and report pages |

---

## 🧭 Navigation

Every page carries a **HOME** button (top-left action button) that returns to the *Executive Control Tower*, plus a page-navigator strip for jumping directly between sections. The intended reading order is:

1. Executive Control Tower
2. Supplier Risk Analysis
3. Supplier Detail
4. Logistics & Delivery
5. Warehouse & Inventory
6. Risk Investigation
7. Business Insights & Recommendations

All visuals are cross-filtered — clicking any bar, dot, or donut slice filters the rest of the page (and drives drill-through where configured).

---

## 🗃️ Data Model

| Table | Role |
|---|---|
| `Fact_SupplyChain` | Transaction-grain fact table — supplier, product, country, shipping cost, lead time, delay probability, risk classification, cargo/weather/customs conditions, order fulfillment status, inventory & demand fields |
| `Dim_Country` | Dimension table that also hosts the report's **DAX measures** (all KPIs are defined here rather than in the fact table) |

### Key DAX measures (defined on `Dim_Country`)

| Measure | Used for |
|---|---|
| `Total Records` | Overall shipment/record volume |
| `Total Shipping cost` / `Average Shipping cost` | Freight cost KPIs |
| `Average Lead Time` | Delivery speed KPI |
| `Average delay probability` | Core delay-risk KPI, reused across almost every page |
| `Average risk score` | Composite risk KPI |
| `High Risk %` / `High Risk Records` | Share and count of shipments classified as high risk |
| `Average Supplier Relaibility` | Supplier scorecard KPI |
| `Average Disruption Likelihood` | Predictive risk KPI |
| `Average Route RisK` | Logistics-route risk KPI |
| `Average Inventory Level` / `Total Historical demand` | Warehouse & inventory KPIs |
| `Average Equipment Availability` / `Average Cargo Condotions` | Warehouse readiness KPIs |

> Note: several measure names retain the source spelling from the original dataset (e.g. *Relaibility*, *Condotions*, *RisK*) — kept as-is to match the model.

---

## 📊 Page-by-Page Breakdown

### 1. Executive Control Tower
*Executive Performance • Risk • Logistics Intelligence*

The landing page — a single-screen summary of the whole supply chain.

- **KPI cards:** Total Records, Total Shipping Cost, Average Lead Time, Average Delay Probability, High Risk %
- **Slicers:** Supplier Country, Risk Classification, Supplier ID — global filters for the page
- **Donut chart:** Record volume by Risk Classification (share of Low/Medium/High risk)
- **Clustered column chart:** Average Delay Probability by Risk Classification
- **Clustered bar chart:** Average Supplier Reliability by Supplier ID
- **Clustered bar chart:** Average Delay Probability by Supplier Country
- **Clustered column chart:** Average Shipping Cost by Risk Classification

**Purpose:** answer "how is the network performing right now, and where's the risk concentrated?" in one glance.

### 2. Supplier Risk Analysis
*Supplier reliability • Risk exposure • Operational performance*

> Identify high-risk suppliers → Assess reliability → Prioritize supplier action

- **KPI cards:** Average Supplier Reliability, High Risk %, High Risk Records
- **Clustered bar chart:** Average Supplier Reliability by Supplier ID
- **Scatter chart:** Supplier Reliability (X) vs. Delay Probability (Y), bubble size = Shipping Cost, colored by Risk Classification, per Supplier ID — a quadrant view for spotting unreliable-and-risky suppliers
- **Column chart:** Record count by Supplier ID, split by Risk Classification
- **Scatter chart:** Supplier Reliability (X) vs. Disruption Likelihood (Y), bubble size = Shipping Cost, per Supplier ID

**Purpose:** rank and triage suppliers by combined reliability and risk signal.

### 3. Supplier Detail
*Deep-dive into supplier performance → Assess risk exposure → Identify corrective actions*

A drill-down page (reached from Supplier Risk Analysis) focused on a single supplier or filtered cohort.

- **KPI cards:** Average Delay Probability, Average Disruption Likelihood, Average Supplier Reliability, Average Shipping Cost, Average Lead Time
- **Bar chart:** Record count by Risk Classification
- **Scatter chart:** Shipping Cost (X) vs. Delay Probability (Y), colored by Risk Classification

**Purpose:** support root-cause conversations with an individual supplier.

### 4. Logistics & Delivery
*Transportation cost • Lead time • Delivery risk*

> Track transportation costs → Identify delivery delays → Optimize logistics performance

- **KPI cards:** Average Shipping Cost, Average Lead Time, Total Shipping Cost, Average Delay Probability
- **Bar chart:** Average Shipping Cost by Supplier Country
- **Scatter chart:** Lead Time (X) vs. Delay Probability (Y), bubble size = Shipping Cost, per Supplier ID
- **Clustered column chart:** Average Shipping Cost by Risk Classification
- **Column chart:** Order Fulfillment Status (sum) by Risk Classification

**Purpose:** connect logistics spend to delivery reliability and find where cost and risk diverge by country/lane.

### 5. Warehouse & Inventory
*Inventory levels • Equipment availability • Operational exposure*

> Assess inventory health → evaluate warehouse readiness → identify operational gaps

- **KPI cards:** Average Inventory Level, Total Historical Demand, Average Equipment Availability, Average Cargo Conditions
- **Scatter chart:** Inventory Level (X) vs. Historical Demand (Y), bubble size = Shipping Cost, per Product ID — flags demand/inventory imbalance
- **Clustered bar chart:** Average Equipment Availability by Supplier Country
- **Clustered column chart:** Average Inventory Level by Risk Classification

**Purpose:** check whether stock levels are aligned to demand and whether warehouse/equipment readiness varies by risk tier.

### 6. Risk Investigation
*Root-cause analysis • Disruption exposure • Delivery risk*

> Trace risk drivers → Uncover root causes → Prioritize mitigation actions

- **KPI cards:** Average Risk Score, Average Disruption Likelihood, Average Delay Probability, High Risk %
- **Donut chart:** Record volume by Risk Classification
- **Scatter chart:** Disruption Likelihood (X) vs. Delay Probability (Y), bubble size = Shipping Cost, per Product ID
- **Clustered bar chart:** Average Route Risk by Risk Classification
- **Scatter chart:** Weather Condition Severity (X) vs. Delay Probability (Y), colored by Risk Classification
- **Scatter chart:** Cargo Condition Status (X) vs. Delay Probability (Y), colored by Risk Classification
- **Scatter chart:** Customs Clearance Time (X) vs. Delay Probability (Y), colored by Risk Classification

**Purpose:** stress-test the usual suspects (weather, cargo condition, customs) against delay probability to see which factors actually explain the risk.

### 7. Business Insights & Recommendations
*From supply chain signals → actionable business decisions*

A narrative summary page (text-based, no charts) that closes the story with findings and a call to action:

- **Overall risk exposure:** ~80% of records are classified High Risk, pointing to significant, network-wide exposure.
- **Supplier risk analysis:** higher supplier risk correlates with *lower* delay probability, and vice versa — a non-linear, counter-intuitive relationship between supplier risk rating and actual delivery performance.
- **Logistics optimization:** shipping costs vary materially by country and by risk tier, pointing to transportation optimization opportunities.
- **Inventory planning:** inventory levels should be re-aligned to historical demand to reduce imbalance.
- **Risk mitigation:** cargo condition, customs clearance time, and weather severity show limited variation across risk tiers — meaning they are **not** the primary drivers of the observed risk (a useful negative finding that redirects mitigation effort elsewhere).

**Overall takeaway:** prioritize supplier risk management and operational monitoring over environmental/logistics factors, since the latter explain less of the variance in risk than expected.

**Closing recommendation:**
> *"Prioritize high-risk suppliers → Strengthen monitoring → Optimize logistics → Reduce disruption and delivery exposure."*

---

## 🔎 Analytical Themes Across the Report

| Theme | Where it shows up |
|---|---|
| **Risk classification** (Low/Medium/High) | Used as the primary color/legend split on nearly every chart, tying every page back to one risk taxonomy |
| **Delay probability** | The most reused single metric — appears on 8+ visuals across 5 pages as the common "outcome" variable |
| **Supplier scorecarding** | Reliability vs. risk vs. cost bubble charts, first at cohort level (page 2) then drilled to individual supplier (page 3) |
| **Cost vs. risk vs. performance trade-offs** | Recurrent scatter-plot pattern (X = driver, Y = delay probability, size = shipping cost) used to test multiple hypotheses (lead time, weather, cargo, customs) against delay outcomes |

---

## 🛠️ How to Use / Extend

1. Open `Supply_Chain_control_tower.pbix` in Power BI Desktop.
2. Use the **Supplier Country**, **Risk Classification**, and **Supplier ID** slicers on the Executive page to filter the whole session (filters persist as you navigate via the page navigator).
3. To point the model at your own data, use **Transform Data / Power Query** to repoint `Fact_SupplyChain`, then refresh — the DAX measures on `Dim_Country` will recalculate automatically as long as column names are preserved.
4. To publish: **File → Publish → Power BI Service**, then set up a scheduled refresh if the source becomes a live connection.

---

GitHub cannot render `.pbix` files inline, so consider adding page screenshots (File → Export → Export report pages as images, or simple screen captures) to a `/screenshots` folder and embedding them above with `![Executive Control Tower](screenshots/executive.png)` for each of the seven pages.
````
