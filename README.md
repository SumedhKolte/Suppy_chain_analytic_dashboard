# Supply Chain Analytics — Just In Time Company

<div align="center">

<img width="1412" alt="Supply Chain Banner" src="https://github.com/user-attachments/assets/8953a71a-a57a-4c41-81dc-dbfd8cd3b3d8" />

<br/>
<br/>

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python)](https://www.python.org/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?style=for-the-badge&logo=powerbi)](https://powerbi.microsoft.com/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas)](https://pandas.pydata.org/)
[![NumPy](https://img.shields.io/badge/NumPy-Scientific%20Computing-013243?style=for-the-badge&logo=numpy)](https://numpy.org/)
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
- [Hypothesis and Issue Trees](#-hypothesis-and-issue-trees)
- [Key Findings](#-key-findings)
- [Recommendations](#-recommendations)
- [Tools and Technologies](#-tools-and-technologies)
- [Getting Started](#-getting-started)

---

## 📖 Project Description

**Just In Time** is an e-commerce company facing critical challenges in its supply chain operations. As the lead data analyst, this project focuses on:

- 🔍 Identifying and diagnosing **supply chain inefficiencies**
- 📦 Analyzing **shipment delays** and **inventory management** issues
- 📊 Building **interactive dashboards** for key business stakeholders
- 💡 Proposing **data-driven structural improvements** to restore and optimize operations

> The dataset covers **order and shipment records**, **inventory data**, and **fulfillment metrics** spanning **3 years (2015–2017)**

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
| 📈 **Sales Manager** | Track customer demand and product sales | Net Sales · Profit · Orders · Top Products |
| 🏭 **Inventory Manager** | Control inventory flow and distribution | Warehouse Inventory · Storage Cost · Fulfillment |
| 🚚 **Shipping Manager** | Oversee daily shipping operations | Orders · Location · Timing · Delay Rate |

---

## 📊 Dashboard Preview

### 🔷 Business Performance Dashboard
> Tracks net sales, profit margin, number of orders, and top-performing product departments over time

<img width="1412" alt="Business Performance Dashboard" src="https://github.com/user-attachments/assets/8953a71a-a57a-4c41-81dc-dbfd8cd3b3d8" />

<br/>

### 🔷 Inventory Management Dashboard
> Monitors warehouse inventory levels, storage costs, order fulfillment timelines, and inventory cost per unit by product

<img width="1413" alt="Inventory Management Dashboard" src="https://github.com/user-attachments/assets/1d290420-2097-4dd4-919d-7acdc8534d3c" />

<br/>

### 🔷 Shipment Management Dashboard
> Analyzes late shipment rates, delay patterns by product department, shipment mode distribution, and geographic shipping data

<img width="1413" alt="Shipment Management Dashboard" src="https://github.com/user-attachments/assets/fdf9c4f6-21d8-4bdf-9b82-044f61c553e9" />

<br/>

### 🔷 Inventory Segmentation ABC-XYZ
> Segments inventory by revenue contribution and demand volatility to prioritize supply chain actions

<img width="1417" alt="Inventory Segmentation" src="https://github.com/user-attachments/assets/fdf9c4f6-21d8-4bdf-9b82-044f61c553e9" />

---

## 🛠️ Data Preprocessing

### Dataset Overview

| Table | Description |
|-------|-------------|
| 📁 `order_and_shipment` | Customer, Order, Shipment and Product information |
| 📁 `inventory` | Warehouse inventory, storage costs, fulfillment data |
| 📁 `fulfillment` | Order fulfillment records |

### Data Cleaning Steps

| Step | Action |
|------|--------|
| 1 | Dropped unnecessary columns `Order Item ID` and `Order Time` |
| 2 | Fixed incorrect data types across all columns |
| 3 | Removed special characters from `Customer Country` column |
| 4 | Checked and handled all missing values |
| 5 | Identified and removed all duplicate records |
| 6 | Resolved product name inconsistencies between order and inventory tables |
| 7 | Removed invalid shipping times less than 0 or greater than 28 days |

> ⚠️ **Note:** 5 product names existed in inventory but had no order records. These were retained due to their significant storage cost contribution

### Feature Engineering

| Feature | Formula |
|---------|---------|
| **Shipping Time** | Shipment Date - Order Date |
| **Delay Shipment** | Late if Shipping Time > Scheduled Days else On Time |
| **Late Shipment Rate** | Total Late Orders / Total Orders |
| **Net Sales** | Gross Sales x (1 - Discount) |
| **Unit Price** | Gross Sales / Order Quantity |
| **Profit Margin** | Total Profit / Total Net Sales |
| **Storage Cost** | Inventory Cost per Unit x Warehouse Inventory |

---

## 📈 Exploratory Data Analysis

<details>
<summary><b>📊 Business Performance Questions</b></summary>
<br>

- What are total net sales, profit, and profit margin?
- How do net sales and profit trend over time?
- Which product departments drive the majority of revenue and orders?
- How do average order quantity and unit price evolve over time?

</details>

<details>
<summary><b>👥 Customer Behavior Questions</b></summary>
<br>

- How are customers distributed by country and market?
- How does the customer base grow over time?
- Are there seasonal or cyclical buying patterns?

</details>

<details>
<summary><b>🛍️ Product Analysis Questions</b></summary>
<br>

- Which categories and product names are most preferred by customers?
- Which categories and product names are most profitable?

</details>

<details>
<summary><b>📦 Inventory Questions</b></summary>
<br>

- Which departments dominate warehouse inventory and storage cost?
- How do warehouse inventory and storage costs change over time?
- What is the average order fulfillment time by department?

</details>

<details>
<summary><b>🚚 Shipment Questions</b></summary>
<br>

- What shipment modes are preferred by customers?
- What is the late shipment rate by department and market?
- How does late shipment rate fluctuate over time?

</details>

---

## 🏷️ Inventory Segmentation

The **ABC-XYZ method** was applied to classify **113 product names**

### ABC Classification — Revenue Contribution

| Segment | Criteria | Description |
|---------|----------|-------------|
| 🔴 **A** | Top 80% of net sales | High Value Products |
| 🟡 **B** | Next 15% of net sales | Medium Value Products |
| 🟢 **C** | Bottom 5% of net sales | Low Value Products |

### XYZ Classification — Demand Volatility

| Segment | CV Range | Demand Type |
|---------|----------|-------------|
| **X** | CV < 0.25 | Regular and Stable Demand |
| **Y** | 0.25 to 0.50 | Variable and Seasonal Demand |
| **Z** | CV > 0.50 | Irregular and Unpredictable Demand |

### Combined Segment Priority

| Segment | Nature | Action |
|---------|--------|--------|
| 🔴 **XA, YA** | High revenue · Stable and Variable demand | Restore immediately — Top Priority |
| 🟡 **XB, XC** | Growing potential · Emerging segments | Monitor closely and invest |
| 🟢 **YB, YC, ZB, ZC** | Low revenue · Irregular demand | Reduce or eliminate inventory |

---

## 🌲 Hypothesis and Issue Trees

### Business Context — SCQ Framework

| Component | Description |
|-----------|-------------|
| **Situation** | Stable revenue and profit from 2015 to mid-2017, driven by Apparel, Golf, Fan Shop and Footwear |
| **Complication** | Sharp operational decline in Q4 2017 — key product departments completely disappeared from sales |
| **Question** | How can the company recover and fix the underlying supply chain weaknesses? |

### Root Cause Analysis Framework
