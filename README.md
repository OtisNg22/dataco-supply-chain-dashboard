# DataCo Supply Chain — Delivery & Profit Dashboard (Power BI)

A four-page Power BI dashboard analysing fulfilment performance and profitability
for a global e-commerce supply chain, built to answer one question:
**where are we losing time and money getting orders to customers, and why?**

> **Headline finding:** late delivery is driven by **shipping mode, not geography**.
> First Class orders are late **95%** of the time while Standard Class is late **38%** —
> yet every world market sits near **55%**. The problem is an unrealistic delivery
> promise on the premium services, not where customers live.

---

## The data

- **Source:** DataCo Smart Supply Chain dataset (Kaggle) — real order-and-shipping data.
- **Size:** 180,519 order lines across 65,752 orders, Jan 2015 – Jan 2018.
- **Note:** the dataset ships with placeholder customer PII (names, emails, passwords).
  These columns were **removed during data preparation** — no personal data is used.

## Tools

- **Power BI Desktop** — model, measures, and report.
- **Power Query (M)** — data cleaning, PII removal, type fixes.
- **DAX** — measures and the calendar table.

## Data model (star schema)

The flat source file was split into a clean star schema:

- **Fact_Orders** — one row per order line (the grain), holding the numbers and keys.
- **Dim_Customer** — 20,652 customers (segment, location).
- **Dim_Product** — 118 products (name, category, department, price).
- **Dim_Date** — a custom calendar (2015–2018), marked as the date table, with
  Auto Date/Time turned off. Order date is the active relationship; shipping date is
  kept as an inactive relationship for ship-date analysis.

## Key measures

Written as explicit DAX measures in a dedicated `_Measures` table:
`Total Sales`, `Total Profit`, `Profit Margin %`, `Total Orders`,
`Late Delivery Rate %`, `Avg Days Real`, `Avg Days Scheduled`, `Avg Shipping Slip`,
`Loss-Making Lines`, `Loss-Making %`, `Total Losses`.

---

## What the dashboard shows

**Overview** — $36.8M sales, $3.97M profit (10.8% margin) over 2015–2017, steady at
about $1M/month. Sales concentrate in a few departments (Fan Shop leads) and in
Europe and LATAM.

**Delivery Performance** — the headline page.
- *Finding:* First Class is late 95% of the time vs 38% for Standard, but every
  market is near 55%.
- *Why it matters:* lateness comes from an unrealistic delivery promise per service,
  not from geography. The premium, paid-for services are the least reliable.
- *Recommendation:* reset the First/Second Class delivery windows to realistic
  targets, or review those carriers. Don't invest in regional fixes — location isn't
  the problem.

**Profit & Leakage**
- *Finding:* 18.7% of order lines lose money (−$3.88M total), but no category is
  net-negative and average discount rate does **not** predict margin.
- *Why it matters:* the leakage is spread thin, not caused by over-discounting.
- *Recommendation:* investigate order-level costs (shipping, returns), not product
  pricing.

**Customer & Market**
- *Finding:* 20,652 customers, mostly the Consumer segment, spread across many
  countries with no dominant market.
- *Why it matters:* a broad base with low concentration risk.
- *Recommendation:* growth comes from fixing delivery and margin, not chasing new
  regions.

---

## A note on the analysis

This dataset is partly synthetic, so several metrics are deliberately uniform
(fraud-style patterns, discount-to-margin links). Rather than invent a story, the
dashboard reports what the data actually supports — including the null results
("discounting is *not* the cause of the losses"), which is itself a useful finding.

## Files

- `DataCo Supply Chain.pbix` — the Power BI report.
- `/screenshots` — page images.
