# End-to-End Retail Customer Behavior & Shopping Trends Analysis

## Project Overview
This portfolio project simulates a real-world, company-level data analytics workflow. Moving beyond basic exploratory data analysis, this project addresses a core business problem statement from a retail use case by executing a complete lifecycle data pipeline: raw data cleaning, robust database analysis, interactive business intelligence dashboarding, corporate reporting, and client-ready presentations.


## Business Problem Statement
A leading retail company aims to better understand its customers' shopping behavior to improve sales, customer satisfaction, and long-term loyalty. The management team has observed shifts in purchasing patterns across demographics, product categories, and sales channels. 

### Overarching Objective:
**"How can the company leverage customer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?"**

---

## Dataset Overview
The analysis utilizes a **Customer Shopping Behavior and Shopping Trends** dataset. Each record tracks an individual customer snapshot and their latest transactional indicators, including:
* **Demographics:** Customer ID, Age, Gender, Location
* **Transaction Details:** Item Purchased, Category, Purchase Amount (USD), Season
* **Preferences & Behavior:** Size, Color, Review Rating, Shipping Type, Payment Method
* **Loyalty & Promos:** Subscription Status, Discount Applied, Previous Purchases, Frequency of Purchases

---

##  Tech Stack & Tools Used
* **Data Processing & Engineering:** Python (`pandas`) via Jupyter Notebook
* **Relational Database Engine:** PostgreSQL / pgAdmin (with setup instructions for MySQL & MS SQL Server)
* **Database Connectivity:** `SQLAlchemy`, `psycopg2`
* **Business Intelligence & Visualization:** Power BI Desktop
* **Documentation & Deliverables:** Gamma AI (Presentation), Microsoft Word (Project Report)

---

##  Step-by-Step Project Workflow

### Step 1: Data Loading & Cleaning (Python)
* Inspected structural metadata, features, data formats, and structural summary statistics.
* **Smart Imputation:** Identified 37 null values in `review_rating`. Instead of a blunt global median, missing values were imputed using the **median rating specific to each product category** to avoid systemic data bias.
* **Standardization:** Converted all mixed-case, spaced column definitions into clean **snake_case** for reliable SQL querying.
* **Feature Engineering:**
    * Binned the `age` feature into balanced quartiles (`young_adult`, `adult`, `middle-aged`, `senior`) using `pd.qcut()`.
    * Mapped structural categorical textual fields (`weekly`, `monthly`, `fortnightly`) into an actionable numeric integer feature (`purchase_frequency_days`).
* **Redundancy Optimization:** Proved data parity between `discount_applied` and `promo_code_used` to drop the redundant vector.

### Step 2: Advanced Business Analysis (SQL)
The processed DataFrame was ingested into a relational PostgreSQL environment using an engineered SQLAlchemy connection wrapper. High-impact business analysis was performed via the following strategic target queries:
1.  **Revenue Split by Gender:** Segmenting overall monetary contributions across customer demographics.
2.  **High-Spend Discount Consumers:** Tracking customers utilizing promotions who still exceeded global spending averages (utilizing SQL Subqueries).
3.  **Top 5 Premium Products:** Filtering items holding peak historical satisfaction ratings (`avg_review_rating`).
4.  **Logistics Value Delta:** Evaluating the average basket value of standard vs. express shipping pipelines.
5.  **Subscription Performance Metrics:** Evaluating whether enrolled subscribers genuinely drive distinct profit metrics compared to standard buyers.
6.  **Promo Reliance Rate:** Analyzing what percentage of specific item volumes rely completely on discounts to convert.
7.  **Customer Loyalty Segmentation:** Engineering a Common Table Expression (CTE) and conditional `CASE` logic to classify customers into `New`, `Returning`, or `Loyal` categories.
8.  **Top 3 Category Performers:** Deploying Window Functions (`ROW_NUMBER() OVER (PARTITION BY...)`) to pull the top three items purchased within each distinct category.
9.  **Subscription Conversion Potential:** Auditing non-subscribed repeat buyers to flag gaps in premium service enrollment.
10. **Demographic Revenue Driver:** Aggregating transactional flows across custom age groups.

### Step 3: Interactive Dashboard Development (Power BI)
Built a fully interactive, cross-filtered executive summary tracking core business KPIs:
* **KPI Scorecards:** Total Unique Customers, Average Order Value (USD), and Average Review Rating calculated using explicit DAX measures.
* **Customer Segmentation:** Donut visuals reflecting subscriber ratios.
* **Sales vs. Revenue Funnels:** Cluster Column Charts illustrating operational transaction counts against exact monetary generation.
* **Demographic Insights:** Horizontal Bar Charts tracking behavioral shifts across dynamic age cohorts.
* **Slicers:** Slicers for `Subscription Status`, `Gender`, `Category`, and `Shipping Type` to enable real-time, self-service data exploration.


##  Key Business Recommendations
Based on the data insights, the following strategic insights were formulated:
1.  **Target High-Value Groups:** Prioritize marketing spend on **Young Adults**, who represent the largest revenue-driving age cohort.
2.  **Optimize Shipping Upsells:** Since **Express Shipping** customers exhibit higher average purchase amounts, introduce premium logistics bundles or loyalty perks around faster delivery options.
3.  **Refine Subscription Offers:** Data reveals a large portion of highly active repeat buyers are not yet subscribers. Revamp the subscription value proposition to actively convert these high-frequency non-subscribers.

---
