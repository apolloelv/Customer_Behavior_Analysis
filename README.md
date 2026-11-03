# Customer Shopping Behavior Analysis

An end-to-end data analytics project: raw shopping data is cleaned and explored in Python, loaded into PostgreSQL, queried with SQL, and presented in a Power BI dashboard, a written report, and a slide deck.

---

## Overview

**Goal:** Understand how customers shop and where revenue comes from, so a retailer can make better decisions on marketing, subscriptions, discounts, and retention.

**Questions this project answers:**
- Which customer groups (gender, age group, loyalty segment) generate the most revenue?
- Do subscribers spend more than non-subscribers?
- Do discounts change how much customers spend?
- Which categories and products perform best?

---

## Dataset

- **File:** `shopping_behavior_updated.csv` (included in this repository)
- **Size:** 3,900 customer records, 18 original columns (no missing values)
- **Key columns:** customer ID, age, gender, item purchased, category, purchase amount (USD), season, review rating, subscription status, shipping type, discount applied, previous purchases, payment method, frequency of purchases

---

## Tools

| Purpose | Tool |
|---|---|
| Loading, cleaning, EDA | Python (pandas, matplotlib), Jupyter Notebook |
| Database | PostgreSQL, pgAdmin 4, SQLAlchemy, psycopg2 |
| Querying | SQL (aggregations, CASE, CTEs, subqueries, window functions) |
| Dashboard | Power BI Desktop |
| Report | Written project report |
| Presentation | NotebookLM |

---

## Steps

1. **Load the data** into pandas and check its structure, data types, and missing values.
2. **EDA:** used summary statistics (`describe`, `info`) and null checks to understand the data.
3. **Clean and engineer features:**
   - Standardized column names (lowercase, underscores) and renamed `purchase_amount_(usd)` to `purchase_amount`
   - Created `age_group` (Young Adult, Adult, Middle-Aged, Senior) using age quartiles
   - Created `purchase_frequency_days` by converting labels like "Weekly" or "Quarterly" into a number of days
   - Found that `promo_code_used` was identical to `discount_applied` in every row, so it was dropped as redundant
4. **Load into PostgreSQL:** wrote the cleaned DataFrame to a `customer` table with SQLAlchemy.
5. **SQL analysis:** answered 10 business questions (see below).
6. **Dashboard:** built an interactive Power BI report connected to the PostgreSQL table.
7. **Report and slides:** summarized the findings in a written report and a NotebookLM presentation.

### SQL questions answered (`customer_behaviour.sql`)

| # | Question |
|---|---|
| 1 | Revenue from male vs. female customers |
| 2 | Discounted purchases that still exceeded the average purchase amount |
| 3 | Top 5 products by average review rating |
| 4 | Average spend: Standard vs. Express shipping |
| 5 | Do subscribers spend more? (customers, revenue, average spend) |
| 6 | Top 5 products by discount rate |
| 7 | Customer segments (New / Returning / Loyal) using a CTE and CASE |
| 8 | Top 3 products within each category using `ROW_NUMBER()` |
| 9 | Are repeat buyers (more than 5 previous purchases) more likely to subscribe? |
| 10 | Revenue contribution by age group |

---

## Dashboard

![Customer Behaviour Dashboard](images/dashboard.png)

**The one-page Power BI dashboard includes:**
- **KPI cards:** 3,900 customers, $59.76 average purchase amount, 3.75 average review rating
- **Subscription split:** donut chart (27% subscribed, 73% not subscribed)
- **Revenue and sales by category:** Clothing leads, followed by Accessories, Footwear, and Outerwear
- **Revenue and sales by age group:** Young Adult, Middle-Aged, Adult, and Senior
- **Slicers:** filter the whole page by subscription status, gender, and category

---

## Results

**Overall:** 3,900 customers, **$233,081** total revenue, **$59.76** average purchase, **3.75** average review rating.

- **Clothing and Accessories drive the business.** They bring in about 77% of revenue (Clothing $104.3K, Accessories $74.2K). Footwear and Outerwear together make up the remaining 23%.
- **Male customers generate about 68% of revenue** ($157.9K vs. $75.2K), because they are 68% of customers. Average spend is nearly the same ($59.54 vs. $60.25).
- **Age groups contribute evenly.** Young Adults lead slightly at $62.1K (about 27% of revenue), but average spend is about $59 to $60 for every group.
- **The customer base is very loyal.** About 80% are Loyal (more than 10 previous purchases), 18% Returning, and only 2% New.
- **Subscribers do not spend more.** Average spend is $59.49 for subscribers vs. $59.87 for non-subscribers, and only 27% of customers are subscribed.
- **Discounts do not increase basket size.** 43% of purchases used a discount, with an average of $59.28 vs. $60.13 without one.
- **Repeat buyers are not more likely to subscribe.** 28% of repeat buyers are subscribed, close to the overall 27%.
- **Top rated products:** Gloves (3.86), Sandals (3.84), Hat (3.81), Boots (3.81), Handbag (3.78).
- **Highest discount rates:** Hat (50%), Sneakers (49.7%), Coat (49.1%), Sweater (48.2%), Pants (47.4%).

**Takeaways**
- Spending is very consistent across segments, so growth is more likely to come from **order volume and retention** than from targeting one demographic.
- Since discounts and subscriptions show no spending lift in this data, their cost-effectiveness is worth reviewing.
- Concentrate marketing and inventory on Clothing and Accessories.

---

## How to Run

**1. Get the project**
Download this repository as a ZIP (green **Code** button, then **Download ZIP**) and extract it, or clone
