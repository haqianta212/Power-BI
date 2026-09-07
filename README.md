# Dashboard of Retail Shop Sales 

A Power BI dashboard project analyzing company sales data to surface revenue trends, profit performance, and the key products, customers, and regions driving business results.

## Overview

The dashboard is built for two audiences, each with a dedicated page:

### 1. Executive Summary (Investors & Business Owners)

Answers high-level questions such as:
- How do monthly revenue and profit trends look?
- Which products, customers, and regions contribute the most revenue?

**Key elements:**
- Annual and monthly revenue/profit trends (line chart with tooltips)
- Total revenue and profit summary cards
- Bar charts for top-contributing products, customers, and regions
- Filters: time slicer, order status = "complete"
- Single-page view (no drill-through)

### 2. Sales & Operations Detail (Sales & Operations Managers)

Answers deeper, diagnostic questions such as:
- Which products/customers contribute the most or least revenue, and why?
- Are revenue changes driven by order volume or pricing?
- What are the monthly order trends for top products and customers, and what's causing them to rise or fall?

**Key elements:**
- Bar charts for top revenue-contributing products and customers
- Line charts for product/customer order trends
- Bar and pie charts to diagnose the causes behind trend changes
- Summary cards for general product/customer info and total orders
- Custom relative-comparison metrics built via a disconnected table and DAX `CALCULATE()` measures (to stay unaffected by report filters)
- Filters: time slicer, clickable bar chart categories, and automatic drill-through filtering into detail pages
- Clicking a product/customer bar drills through to dedicated **Product Details** and **Customer Details** pages

## Data Cleaning & Preparation

Raw sales data required several cleaning steps before modeling:

- **Text formatting:** Trimmed and standardized capitalization; removed extra internal spaces from province names (split → trim → merge columns)
- **Duplicates:** Removed duplicate rows
- **Invalid/null Customer IDs:** Removed (affected only 2 rows)
- **Null discount values:** Recalculated via a custom Power Query M function based on quantity, unit price, and sales amount
- **Inconsistent date formats:** Split into dash- and slash-separated groups; slash-formatted dates were parsed as US or UK date format based on the month range implied by each source file's name; rows with ambiguous date ranges were removed
- **Fragmented source files:** Multiple sales tables combined via append

**Key DAX measures created:**
- Total Order, Total Revenue (Sales Amount), Total Cost (Quantity × Unit Price)
- Total Profit = Total Revenue − Total Cost
- Gross Profit Margin = Total Profit / Total Revenue

## Key Insights

- Annual revenue trend is stable; monthly revenue shows a seasonal pattern. Profit averages roughly **20% of revenue** per month.
- **Top contributors:**
  - Product: **Laptop Pro**
  - Customer: **Sentosa Group**
  - Region: **Jawa Timur (East Java)**
- Laptop Pro (TechPro) has a below-average order count — its high revenue comes from its premium price rather than order volume.
- The recent decline in Laptop Pro orders is likely due to customers shifting to other computer subcategory products, along with a slight price increase. Recent returned orders also warrant further investigation.
- Sentosa Group generates substantial revenue but orders relatively infrequently (below-average order count per customer).
- The recent decline in Sentosa Group's order volume does not appear to be driven by cancelled/returned orders or price increases on frequently purchased products — the cause requires further investigation.

## Tech Stack

- **Power BI** — data modeling, DAX measures, dashboard visualization
- **Power Query (M)** — data cleaning and transformation

---
*This README was generated from the project's final presentation slides.*
