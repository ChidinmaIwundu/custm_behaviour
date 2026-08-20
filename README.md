# Customer Shopping Behavior Analysis

A data analytics project that turns 3,900 raw retail transactions into actionable business insights — covering data cleaning, SQL analysis, and an interactive Power BI dashboard.

---

## Overview

This project analyzes customer shopping behavior using transactional data from 3,900 purchases across multiple product categories. 

The workflow spans the full analytics stack: **Python** for cleaning and exploration, **PostgreSQL** for structured querying, and **Power BI** for stakeholder-facing visualization.

---

## Dataset

| | |
|---|---|
| **Rows** | 3,900 |
| **Columns** | 18 |
| **Missing data** | 37 values in `review_rating` |

**Key features:**
- **Customer demographics:** Age, Gender, Location, Subscription Status
- **Purchase details:** Item Purchased, Category, Purchase Amount, Season, Size, Color
- **Shopping behavior:** Discount Applied, Promo Code Used, Previous Purchases, Frequency of Purchases, Review Rating, Shipping Type

---

## Tools

- **Python** (pandas) — data loading, cleaning, feature engineering
- **PostgreSQL** — structured SQL analysis
- **Power BI** — interactive dashboard and visualization
- **Gamma** — presentation deck summarizing findings for non-technical stakeholders

---

## Steps

1. **Data Loading** — Imported the raw dataset with pandas; used `df.info()` and `.describe()` to profile structure and summary statistics.
2. **Data Cleaning**
   - Imputed the 37 missing `review_rating` values using the median rating per product category.
   - Standardized all column names to `snake_case`.
   - Checked `discount_applied` vs `promo_code_used` for redundancy and dropped the duplicate column.
3. **Feature Engineering**
   - Created `age_group` by binning customer ages.
   - Created `purchase_frequency_days` from purchase frequency data.
4. **Database Integration** — Loaded the cleaned DataFrame into PostgreSQL for structured SQL analysis.
5. **SQL Analysis** — Answered targeted business questions (revenue by segment, high-value customers, top-rated products, shipping and subscription comparisons — see Results below).
6. **Dashboard Build** — Designed an interactive Power BI dashboard with filters for subscription status, gender, category, and shipping type.

---

## Dashboard

The Power BI dashboard lets stakeholders slice performance by **subscription status, gender, category, and shipping type**, with KPI cards and visuals for:

- Number of customers, average review rating, and average purchase amount
- % of customers by subscription status
- Revenue and sales by category
- Revenue by age group

> Add your exported dashboard image at `assets/dashboard.png` and it will render here:
> `![Dashboard](assets/dashboard.png)`

**Headline KPIs:**
| Metric | Value |
|---|---|
| Number of Customers | 3.9K |
| Average Review Rating | 3.75 |
| Average Purchase Amount | $59.76 |

---

## Results

Key findings from the SQL analysis:

- **Revenue by Gender** — Male customers generated **$157,890** in revenue vs. **$75,191** from female customers.
- **High-Spending Discount Users** — 839 customers used a discount and still spent above the average purchase amount, indicating discount-driven behavior doesn't always mean price sensitivity.
- **Top 5 Products by Rating** — Gloves (3.86), Sandals (3.84), Boots (3.82), Hat (3.80), and Skirt (3.78) led average review ratings.
- **Shipping Type Comparison** — Express shipping customers spent slightly more on average ($60.48) than Standard shipping customers ($58.46).
- **Subscribers vs. Non-Subscribers** — Non-subscribers (2,847 customers) drove **$170,436** in total revenue vs. **$62,645** from subscribers (1,053 customers), though average spend per customer was nearly identical (~$59-60) — subscriber value comes from volume potential, not higher basket size.

**Business Recommendations:**
- Boost subscriptions by promoting exclusive subscriber-only benefits.
- Build loyalty programs to convert repeat buyers into a "Loyal" segment.
- Review discount policy to balance sales lift against margin control.
- Lead campaigns with top-rated and best-selling products.
- Target marketing toward high-revenue age groups and express-shipping users.

---

## How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/ChidinmaIwundu/customer-shopping-behavior-analysis.git
   cd customer-shopping-behavior-analysis
   ```

2. **Install Python dependencies**
   ```bash
   pip install pandas numpy sqlalchemy psycopg2-binary
   ```

3. **Set up PostgreSQL**
   - Create a local database (e.g. `customer_analysis`).
   - Update the database connection string in `load_to_postgres.py` with your credentials.

4. **Run the cleaning and load script**
   ```bash
   python clean_and_load.py
   ```
   This cleans the raw CSV and loads the resulting `public.customer` table into PostgreSQL.

5. **Run the SQL analysis**
   - Open `analysis_queries.sql` in pgAdmin (or your preferred client) and run the queries to reproduce the results above.

6. **Explore the dashboard**
   - Open `dashboard.pbix` in Power BI Desktop to interact with the filters and visuals directly.

---

## Repository Structure

```
customer-shopping-behavior-analysis/
├── data/
│   └── raw_customer_data.csv
├── clean_and_load.py
├── analysis_queries.sql
├── dashboard.pbix
├── assets/
│   └── dashboard.png
└── README.md
