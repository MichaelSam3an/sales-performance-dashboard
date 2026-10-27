<div align="center">

# Enterprise Sales Analytics & Performance Dashboard

**A four-page, interactive Power BI report that turns 1,000 transactions (~$5.02M in sales) into decisions on trends, regions, products and customers.**

[![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/desktop/)
![DAX](https://img.shields.io/badge/DAX-Measures-0F766E?style=for-the-badge)
![Power Query](https://img.shields.io/badge/Power%20Query-M-2563EB?style=for-the-badge)
![Report pages](https://img.shields.io/badge/Report%20pages-4%20%2B%202%20hidden-7C3AED?style=for-the-badge)
![Dataset](https://img.shields.io/badge/Dataset-1%2C000%20rows-64748B?style=for-the-badge)

[Overview](#-overview) · [Key Insights](#-key-business-insights) · [Dashboard Pages](#-dashboard-architecture) · [Data Model](#-data-model) · [Interactivity](#-interactivity--advanced-features) · [Getting Started](#-getting-started) · [Docs](#-documentation)

</div>

<!--
Add 4 page screenshots to assets/screenshots/ and uncomment:

<p align="center">
  <img src="assets/screenshots/01_overview.png" width="48%" />
  <img src="assets/screenshots/02_regions_reps.png" width="48%" />
</p>
<p align="center">
  <img src="assets/screenshots/03_product_categories.png" width="48%" />
  <img src="assets/screenshots/04_customers_channels.png" width="48%" />
</p>
-->

---

## 📌 Overview

Sales leaders usually have the data but not a single place to answer four questions quickly:

1. **How are sales trending**, and is growth accelerating or stalling?
2. **Where and who** is driving revenue: which regions and sales reps?
3. **What** sells: which product categories, at what discount level and margin?
4. **To whom and how**: new vs. returning customers, online vs. retail, payment preferences?

This dashboard answers all four on a consistent 1920 × 1080 canvas, with global slicers, drill-down, drill-through to rep-level transactions, and hover tooltips.

| | |
|---|---|
| **Period covered** | 1 Jan 2023 – 1 Jan 2024 |
| **Grain** | One row per sales transaction (1,000 rows) |
| **Total sales** | $5,019,265 (≈ $5.02M) |
| **Dimensions** | 4 regions · 5 sales reps · 4 product categories · 100 product IDs · 2 customer types · 3 payment methods · 2 sales channels |
| **Tech stack** | Power BI Desktop · Power Query (M) · DAX · JSON theme |

---

## 💡 Key Business Insights

Findings below come from the dataset behind the dashboard. Pages 1 and 3 exclude a 3-row, one-day stub (1 Jan 2024, $19.3K), so their totals read **$4.999M**; pages 2 and 4 show the full **$5.019M**. See [Data notes](#-data-notes--design-decisions).

| Theme | Finding |
|---|---|
| **Revenue is stable, not seasonal** | Monthly sales average ~$417K. January 2023 was the peak ($476K) and September 2023 the low ($368K). H1 ($2.49M) and H2 ($2.51M) are within 0.5% of each other. |
| **North leads, South trails** | North generates **$1.37M (27.3%)**, about 19% more than South at **$1.15M (23.0%)**. East and West sit in between at 25.1% and 24.6%. |
| **Rep performance varies the most** | Rep spread is the widest of any dimension: David leads at **$1.14M (22.7%)**, 33% above Charlie at **$0.86M (17.2%)**. Bob is second in sales but has the lowest unit margin (8.5% vs. 9.7% for Alice). |
| **Clothing wins on revenue, not margin** | Clothing is the top category (**$1.31M, 26.2%**) yet has the thinnest unit margin (8.9%). Furniture earns the highest (9.7%). Electronics carries the lightest average discount (13.6% vs. 16.0% for Clothing). |
| **Heavy discounting is the norm** | The 20–30% discount band holds the most transactions (38%) and the most revenue (39.6% of sales). Average discount is 15.2%. |
| **Balanced customer and channel mix** | New customers account for 49.9% of sales and online for 49.0%. Credit card is the most-used payment method (35.0%), followed by bank transfer (34.2%) and cash (30.8%). |
| **Regional customer mix differs** | New customers make up 55.7% of North and 53.9% of East sales, but only 44.9% of South and 44.2% of West, which suggests different acquisition vs. retention dynamics. |

> **Reading the numbers:** differences across categories, channels and customer types are modest, so rep mix and regional customer mix are where the dashboard shows the most leverage.

---

## 🏗 Dashboard Architecture

```mermaid
flowchart LR
    A[sales_clean.csv] --> B[Power Query<br/>typed load]
    B --> C[(Sales table<br/>1,000 rows)]
    D[Date table<br/>DAX calculated] -->|1 to many| C
    C --> E[DAX measures]
    D --> E
    E --> P1[Overview]
    E --> P2[Regions & Reps]
    E --> P3[Product Categories]
    E --> P4[Customers, Channels & Payments]
    P2 -.drill-through.-> H1[Rep Detail<br/>hidden]
    P4 -.tooltip.-> H2[TT_SalesTrend<br/>hidden]
