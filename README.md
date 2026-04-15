```markdown
# Supply Chain Analytics — Just In Time Company

<div align="center">

![Supply Chain Banner]
<img width="1412" height="735" alt="Image" src="https://github.com/user-attachments/assets/8953a71a-a57a-4c41-81dc-dbfd8cd3b3d8" />
<img width="1413" height="733" alt="Image" src="https://github.com/user-attachments/assets/1d290420-2097-4dd4-919d-7acdc8534d3c" />

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python)](https://www.python.org/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?style=for-the-badge&logo=powerbi)](https://powerbi.microsoft.com/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas)](https://pandas.pydata.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

</div>

---

## 📌 Table of Contents

- [Project Description](#-project-description)
- [Methodology](#-methodology)
- [Dashboard Preview](#-dashboard-preview)
- [Data Preprocessing](#-data-preprocessing)
- [Exploratory Data Analysis](#-exploratory-data-analysis)
- [Inventory Segmentation](#-inventory-segmentation)
- [Hypothesis & Issue Trees](#-hypothesis--issue-trees)
- [Key Findings](#-key-findings)
- [Recommendations](#-recommendations)
- [Project Structure](#-project-structure)
- [Tools & Technologies](#-tools--technologies)
- [Getting Started](#-getting-started)

---

## 📖 Project Description

**Just In Time** is an e-commerce company facing critical challenges in its supply chain operations. As the lead data analyst, this project focuses on:

- 🔍 Identifying and diagnosing **supply chain inefficiencies**
- 📦 Analyzing **shipment delays** and **inventory management** issues
- 📊 Building **interactive dashboards** for key business stakeholders
- 💡 Proposing **data-driven structural improvements** to restore and optimize operations

The dataset covers **order & shipment records**, **inventory data**, and **fulfillment metrics** spanning 3 years (2015–2017).

---

## 🧪 Methodology

| Component | Details |
|-----------|---------|
| **Analysis Type** | Descriptive · Exploratory · Diagnostic |
| **Tools** | Python · Power BI |
| **Python Libraries** | Pandas · NumPy · Matplotlib · Seaborn · Scikit-learn |

### Stakeholder Requirements

| Stakeholder | Objective | Dashboard Focus |
|-------------|-----------|-----------------|
| 📈 **Sales Manager** | Track customer demand & product sales | Net Sales · Profit · Orders · Top Products |
| 🏭 **Inventory Manager** | Control inventory flow & distribution | Warehouse Inventory · Storage Cost · Fulfillment |
| 🚚 **Shipping Manager** | Oversee daily shipping operations | Orders · Location · Timing · Delay Rate |

---

## 📊 Dashboard Preview

### 🔷 Business Performance Dashboard
> Tracks net sales, profit margin, number of orders, and top-performing product departments over time.

![Business Performance](<img width="1412" height="735" alt="Image" src="https://github.com/user-attachments/assets/8953a71a-a57a-4c41-81dc-dbfd8cd3b3d8" />)

---

### 🔷 Inventory Management Dashboard
> Monitors warehouse inventory levels, storage costs, order fulfillment timelines, and inventory cost per unit by product.

![Inventory Management](https://github.com/hoshigan/Supply-Chain-Analytic---Just-In-Time-Company/assets/139525944/c1f801eb-da1f-408a-972e-6b8ffee3398c)

---

### 🔷 Shipment Management Dashboard
> Analyzes late shipment rates, delay patterns by product department, shipment mode distribution, and geographic shipping data.

![Shipment Management](<img width="1413" height="733" alt="Image" src="https://github.com/user-attachments/assets/1d290420-2097-4dd4-919d-7acdc8534d3c" />)

---

### 🔷 Inventory Segmentation (ABC-XYZ)
> Segments inventory by revenue contribution and demand volatility to prioritize supply chain actions.

![Inventory Segmentation](<img width="1417" height="730" alt="Image" src="https://github.com/user-attachments/assets/fdf9c4f6-21d8-4bdf-9b82-044f61c553e9" />)

---

## 🛠️ Data Preprocessing

### Dataset Overview

The dataset consists of **three tables**:

```
📁 order_and_shipment   →  Customer, Order, Shipment & Product information
📁 inventory            →  Warehouse inventory, storage costs, fulfillment data
📁 fulfillment          →  Order fulfillment records
```

### Data Cleaning Steps

| Step | Action |
|------|--------|
| 1 | Dropped unnecessary columns (`Order Item ID`, `Order Time`) |
| 2 | Fixed incorrect data types across columns |
| 3 | Removed special characters from `Customer Country` |
| 4 | Checked and handled missing values |
| 5 | Identified and removed duplicate records |
| 6 | Resolved product name inconsistencies between order & inventory tables |
| 7 | Removed invalid shipping times (`< 0` or `> 28` days) |

> ⚠️ **Note:** 5 product names existed in inventory but had no order records. These were retained due to their significant storage cost contribution.

### Feature Engineering

```python
# Datetime Features
Order Date    = Day + Month + Year (combined)
Shipment Date = Day + Month + Year (combined)

# Shipment Features
Shipping Time      = Shipment Date - Order Date
Delay Shipment     = "Late" if Shipping Time > Scheduled Days, else "On Time"
Late Shipment Rate = Total Late Orders / Total Orders

# Business Performance Features
Net Sales      = Gross Sales × (1 - Discount)
Unit Price     = Gross Sales / Order Quantity
Profit Margin  = Total Profit / Total Net Sales

# Inventory Features
Storage Cost   = Inventory Cost per Unit × Warehouse Inventory
```

---

## 📈 Exploratory Data Analysis

### Business Performance Questions
- What are total net sales, profit, and profit margin?
- How do net sales and profit trend over time?
- Which product departments drive the majority of revenue and orders?
- How do average order quantity and unit price evolve?

### Customer Behavior Questions
- How are customers distributed by country and market?
- How does the customer base grow over time?
- Are there seasonal or cyclical buying patterns?

### Product Analysis Questions
- Which categories and product names are most preferred?
- Which categories and product names are most profitable?

### Inventory Questions
- Which departments dominate warehouse inventory and storage cost?
- How do warehouse inventory and storage costs change over time?
- What is the average order fulfillment time by department?

### Shipment Questions
- What shipment modes are preferred by customers?
- What is the late shipment rate by department and market?
- How does late shipment rate fluctuate over time?

---

## 🏷️ Inventory Segmentation

The **ABC-XYZ method** was applied to classify 113 product names:

### ABC Classification (Revenue Contribution)

| Segment | Criteria |
|---------|----------|
| **A** — High Value | Top 80% of total net sales |
| **B** — Medium Value | Next 15% of net sales |
| **C** — Low Value | Bottom 5% of net sales |

### XYZ Classification (Demand Volatility via Coefficient of Variation)

| Segment | CV Range | Demand Type |
|---------|----------|-------------|
| **X** | CV < 0.25 | Regular / Stable |
| **Y** | 0.25 ≤ CV ≤ 0.5 | Variable / Seasonal |
| **Z** | CV > 0.5 | Irregular / Unpredictable |

### Segment Behavior Summary

| Segment | Nature | Priority |
|---------|--------|----------|
| **XA, YA** | High revenue · Stable/Variable demand | 🔴 Critical — Restore immediately |
| **XB, XC** | Growing potential · Emerging segments | 🟡 Monitor & invest |
| **YB, YC, ZB, ZC** | Low revenue · Irregular demand | 🟢 Reduce or eliminate |

---

## 🌲 Hypothesis & Issue Trees

### Business Context

| | Description |
|--|--|
| **Situation** | Stable revenue & profit from 2015 to mid-2017, driven by Apparel, Golf, Fan Shop, Footwear |
| **Complication** | Sharp operational decline in Q4/2017 — key product departments disappeared from sales |
| **Question** | How can the company recover and address underlying supply chain weaknesses? |


### Four Hypotheses Tested

```
┌─────────────────────────────────────────────────────────────────┐
│  SUPPLY CHAIN PROBLEM — ROOT CAUSE ANALYSIS                     │
├──────────────┬──────────────────────────────────────────────────┤
│  External    │  H1: Customers changed product preferences       │
│  Factors     │  H2: Suppliers failed to deliver products        │
├──────────────┼──────────────────────────────────────────────────┤
│  Internal    │  H3: Company intentionally changed product mix   │
│  Factors     │  H4: High late shipment rate eroded loyalty      │
└──────────────┴──────────────────────────────────────────────────┘
```

### Hypothesis Conclusions

| # | Hypothesis | Verdict | Reasoning |
|---|-----------|---------|-----------|
| H1 | Customers changed preferences | ❌ Unlikely | Supply dropped before demand fell; customer base too small for mass preference shift |
| H2 | Supplier delivery failure | ✅ Most Likely | Abrupt disappearance of XA/YA segments without prior warning |
| H3 | Company changed product offerings | ⚠️ Possible | Removing 80% revenue products abruptly is irrational; needs further data |
| H4 | Late shipment impacted loyalty | ❌ Unlikely | LSR was persistently high before Q4/2017 without impacting revenue |

---

## 🔑 Key Findings

<details>
<summary><b>📊 Business Performance</b></summary>

- Total net sales of **~$5.5M** and profit of **~$4M** over 3 years, yielding a strong **72% profit margin**
- A **sharp decline in Q4/2017** — both revenue and orders collapsed simultaneously
- The decline was driven by the **disappearance of top-selling departments**: Apparel, Fan Shop, Footwear, and Golf
- Since costs and revenues declined proportionally, the issue is clearly **revenue-side**, not cost-driven

</details>

<details>
<summary><b>👥 Customer Behavior</b></summary>

- Customer market composition **shifted cyclically** over time (Europe → Asia Pacific → North America)
- Despite market shifts, **overall ordering demand remained relatively stable**
- The customer base grew to approximately **~8,000 unique customers** over the period

</details>

<details>
<summary><b>📦 Inventory Management</b></summary>

- The company **frequently overstocked** — inventory ran up to **30% above actual demand** even during decline periods
- Best-selling products (XA, YA segments) had the **longest replenishment lead times**, making them most vulnerable
- Newer segments (Technology, Health & Beauty) had **shorter fulfillment times**
- Storage costs mirrored the revenue decline, suggesting inventory was disrupted simultaneously

</details>

<details>
<summary><b>🚚 Shipment Operations</b></summary>

- **Late Shipment Rate (LSR) averaged ~40%** consistently across all 3 years
- LSR was uniformly high regardless of **product department or geographic market**
- This persistent inefficiency **predates** the Q4/2017 incident, suggesting systemic delivery issues
- Many orders selecting **fast shipping modes** (Same Day, First Class) were still shipped days later

</details>

---

## 💡 Recommendations

### 1️⃣ Restore Revenue — By Inventory Segment

#### 🔴 XA & YA Segments — Critical Priority
> These segments historically generated **80% of net sales**

- Immediately investigate and identify the **root cause of the supply disruption**
- Source and validate **alternative suppliers** (e.g., Southeast Asia/Central America for Apparel; North America/East Asia for Electronics)
- **Redesign supply chain resilience**: multi-sourcing, safety stock agreements, supplier risk scoring

#### 🟡 XB & XC Segments — Growth Priority
> These segments **sustained all revenue** during the disruption period

- Conduct **market research** to quantify demand potential
- Analyze local and global market trends for **expansion opportunities**
- Implement **demand forecasting** and monitor segment evolution closely

#### 🟢 YB, YC, ZB, ZC Segments — Optimize
> Low revenue contribution, high demand irregularity

- **Reduce or eliminate** inventory for these segments
- Reallocate warehouse space and capital to higher-value segments

---

### 2️⃣ Reduce Overstock & Prevent Stockouts

```
✅ Implement demand forecasting using historical sales data + market trends
✅ Set dynamic reorder points per product (based on lead time + sales velocity)
✅ Maintain calibrated safety stock levels per segment
✅ Leverage cyclical customer market patterns for inventory planning:
   - Q4 2017 → Asia Pacific dominant
   - Q1 2018 → Asia Pacific expected to continue
   - Following quarters → North America expected to rise
```

---

### 3️⃣ Reduce Late Shipment Rate (Currently ~40%)

| Action | Description |
|--------|-------------|
| 🔄 **Route Optimization** | Redesign transportation routes; adopt cross-docking strategies |
| 🤝 **Local Logistics Partners** | Collaborate with regional carriers in distant markets |
| 🏭 **Strategic Warehouse Expansion** | Establish a logistics hub in **Singapore** for Asia Pacific markets |
| 📡 **Real-Time Tracking** | Implement order tracking visibility to identify delays proactively |

---

---

## 🔧 Tools & Technologies

| Category | Tool / Library |
|----------|---------------|
| **Language** | Python 3.8+ |
| **Data Manipulation** | Pandas · NumPy |
| **Visualization (EDA)** | Matplotlib · Seaborn · Plotly |
| **Segmentation** | Scikit-learn |
| **BI Dashboard** | Microsoft Power BI |
| **Version Control** | Git · GitHub |

---

## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/SumedhKolte/Suppy_chain_analytic_dashboard.git

# Navigate to project directory
cd Suppy_chain_analytic_dashboard

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter Notebook
jupyter notebook
```

> 📊 To view the Power BI dashboard, open `Interactive Dashboard.pbix` in **Microsoft Power BI Desktop**

---

<div align="center">

**Made by [sumedhkolte](https://github.com/SumedhKolte)**

⭐ If you found this project helpful, please consider giving it a star!

</div>
```
