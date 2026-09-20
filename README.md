# Customer Sales Intelligence

**End-to-end analytics project: Python → PostgreSQL → Power BI → Business Insights**

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Excel-217346?logo=microsoftexcel&logoColor=white)

---

## Table of Contents

- [Project Overview](#project-overview)
- [Key Results](#key-results)
- [Tools & Technologies](#tools--technologies)
- [Project Structure](#project-structure)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Dashboard Preview](#dashboard-preview)
- [Key Business Insights](#key-business-insights)
- [Business Recommendations](#business-recommendations)
- [Skills Demonstrated](#skills-demonstrated)
- [Author](#author)

---

## Project Overview

**Customer Sales Intelligence** analyzes customer behavior, sales performance, profitability, product performance, and business operations, turning raw transactional data into actionable business insights and recommendations.

**Business questions answered:**

- How is the business performing overall?
- Which products generate the most sales and profit?
- Which customers contribute the most revenue, and which are at risk of becoming inactive?
- How does customer value differ across segments?
- How do discounts affect sales and profitability?
- Which payment methods perform better?
- How do cancellations and returns affect operations?
- How do sales and profitability change over time?

---

## Key Results

| Metric | Value |
|--------|-------|
| Total Sales | 609.53M |
| Total Profit | 84.98M |
| Profit Margin | 13.94% |
| Total Orders | 10,000 |
| Total Customers | 1,498 |
| Average Order Value | 60,952.82 |
| Delivery / Cancellation / Return Rate | 91.20% / 4.96% / 3.84% |

---

## Tools & Technologies

| Tool | Purpose |
|------|---------|
| Python (Pandas, NumPy, Matplotlib) | Data cleaning, EDA, customer segmentation, RFM analysis |
| PostgreSQL + pgAdmin | SQL-based business analysis |
| Power BI | Interactive dashboards |
| Excel | Initial data inspection and validation |
| GitHub | Documentation and portfolio presentation |

---

## Project Structure

```text
Customer_Sales_Intelligence/
│
├── Python/
│   └── Customer_Sales_Intelligence.ipynb
│
├── PostgreSQL/
│   └── SQL_Analysis.sql
│
├── PowerBI/
│   └── Customer_Sales_Intelligence.pbix
│
├── screenshots/
│   ├── 01_executive_overview.png
│   ├── 02_product_performance.png
│   ├── 03_customer_intelligence.png
│   └── 04_business_performance.png
│
├── Data/
│   └── Customer_Sales_Intelligence_cleaned.xlsx
│
└── README.md
```

---

## Dataset

E-commerce transactional dataset with **10,000 orders** and approximately **1,500 customers**.

| Column | Description |
|--------|-------------|
| Order_ID | Unique order identifier |
| Order_Date | Date of the order |
| Customer_ID | Unique customer identifier |
| Product_ID | Unique product identifier |
| Quantity | Number of products purchased |
| Discount | Discount applied to the order |
| Sales | Revenue generated from the order |
| Profit | Profit generated from the order |
| Payment_Method | Payment method used |
| Order_Status | Current status of the order |

---

## Methodology

### 1. Data Preparation & Validation

Checks performed: data types, missing values, duplicates, unique Order IDs, and quantity, discount, sales, profit, payment method, order status, and business-rule validation.

**Key findings:**

- A small number of undefined payment methods were labeled **Unknown** instead of being deleted, preserving the original transactions.
- Cancelled and returned orders have zero recorded sales and profit, so they were treated as operational outcomes rather than assuming direct financial losses.

### 2. Python Analysis

- **Business KPIs:** orders, customers, sales, profit, average order value, profit margin, delivery / cancellation / return rates
- **Monthly analysis:** sales, profit, orders, margin, month-over-month growth
- **Product analysis:** sales, profit, margin, quantity, ranking
- **Customer analysis:** sales, profit, order frequency, average order value, margin

### 3. Customer Value Segmentation

| Segment | Customers | Orders | Sales | Profit Margin |
|---------|-----------|--------|-------|---------------|
| Low Value | 500 | 2,472 | 67.86M | 16.36% |
| Medium Value | 499 | 3,451 | 178.56M | 14.38% |
| High Value | 499 | 4,077 | 363.11M | 13.28% |

High-value customers generated about **59.6% of total sales**.

### 4. RFM Analysis

**Recency** (how recently a customer purchased), **Frequency** (how often), **Monetary** (how much).

| Segment | Customers | Orders | Historical Sales |
|---------|-----------|--------|------------------|
| Loyal Customers | 444 | 3,522 | 192.59M |
| Champions | 188 | 1,821 | 136.95M |
| At Risk | 267 | 2,113 | 129.82M |
| Lost Customers | 323 | 1,337 | 75.55M |
| New Customers | 170 | 751 | 47.72M |
| Potential Customers | 106 | 456 | 26.91M |

### 5. Customer Profitability & CLV-Style Analysis

Some customers generated more than 1M in sales but had margins of only 10–12%, while some lower-revenue customers achieved considerably higher margins. A simplified CLV-style analysis (total sales, total profit, number of orders, average order value, profit margin) was used to identify customers with stronger long-term value.

### 6. PostgreSQL Analysis

```sql
CREATE TABLE orders (
    Order_ID VARCHAR(20) PRIMARY KEY,
    Order_Date DATE,
    Customer_ID VARCHAR(20),
    Product_ID VARCHAR(20),
    Quantity INTEGER,
    Discount DECIMAL(5,2),
    Sales DECIMAL(15,2),
    Profit DECIMAL(15,2),
    Payment_Method VARCHAR(50),
    Order_Status VARCHAR(30)
);
```

SQL techniques used: aggregations, conditional logic (CASE), CTEs, window functions, NTILE segmentation, ranking, month-over-month growth, RFM, customer segmentation, and correlation analysis.

### 7. Correlation Analysis

| Relationship | Correlation |
|--------------|-------------|
| Sales vs Profit | 0.9466 |
| Discount vs Sales | -0.0552 |
| Discount vs Profit | -0.0645 |

Sales and profit are strongly positively related, while discount shows only a weak negative relationship with sales and profit. Correlation indicates association, not causation.

---

## Dashboard Preview

The Power BI report contains four analytical pages.

### Page 1: Executive Overview

High-level business performance: Total Sales, Total Profit, Profit Margin, Total Orders, Total Customers, Monthly Sales Trend, Sales vs Profit, Order Status, and Region-wise Sales.

![Executive Overview](screenshots/01_executive_overview.png)

### Page 2: Product Performance

Top 10 Products by Sales and Profit, Category Performance, Product Profit Margin, and Quantity vs Sales. Identifies high-revenue, high-profit, and high-margin products, and where sales and profitability differ.

![Product Performance](screenshots/02_product_performance.png)

### Page 3: Customer Intelligence

Top 10 Customers by Sales, RFM Segment Count and Sales, Customer Value Segment Count and Sales. Shows customer contribution, loyalty, retention opportunities, and at-risk customers.

![Customer Intelligence](screenshots/03_customer_intelligence.png)

### Page 4: Business Performance

Payment Method Analysis, Order Status Analysis, Discount Analysis, Monthly Profit Margin, and Executive KPI Cards. Focuses on payment behavior, fulfillment issues, discount patterns, and profitability trends.

![Business Performance](screenshots/04_business_performance.png)

---

## Key Business Insights

1. **December was the strongest month:** about 59.08M in sales and 8.20M in profit. February was the lowest at about 43.00M.
2. **Growth was uneven:** the strongest month-over-month increases were March (+19.34%), December (+18.26%), and July (+11.37%).
3. **High sales do not always mean high profit:** PROD-018 generated 26.29M in sales at an 8.16% margin, while PROD-054 generated 23.40M at a 17.05% margin.
4. **High-value customers drive revenue:** 363.11M in sales, about 59.6% of the total, making retention critical.
5. **At-Risk customers are a major opportunity:** 267 customers with about 129.82M in historical sales but weaker recent engagement.
6. **Loyal Customers are the largest RFM segment:** 444 customers and about 192.59M in historical sales, a strong base for retention and cross-selling.
7. **Revenue and profitability differ:** several high-sales customers have low margins, so customers should be evaluated on revenue, profit, margin, and purchase frequency together.
8. **Payment methods differ:** bKash had the highest transaction volume and sales contribution, while Card users had the highest observed margin at about 14.03%.
9. **Fulfillment needs monitoring:** about 8.8% of orders were cancelled or returned. Because the dataset records zero sales and profit for these orders, direct financial loss should not be assumed without additional cost data.
10. **Discounts are not consistently effective:** weak negative correlations with sales and profit suggest discounts should be targeted, not applied broadly.

---

## Business Recommendations

| # | Recommendation | Suggested Actions |
|---|----------------|-------------------|
| 1 | **Prioritize high-value customer retention** | Personalized offers, loyalty benefits, early access, repeat-purchase campaigns, personalized recommendations |
| 2 | **Launch reactivation campaigns for At-Risk customers** | Reactivation emails, targeted offers, limited-time incentives, purchase-based recommendations, reminders. Goal: move them back to Loyal or Champion |
| 3 | **Optimize product profitability** | Review pricing, supplier cost, discount level, operational cost, and positioning of high-sales, low-margin products |
| 4 | **Replace blanket discounts with targeted discounts** | Target by customer segment, RFM segment, purchase history, product margin, and customer profitability |
| 5 | **Improve cancellation and return management** | Investigate reasons, product-level patterns, delivery issues, customer-level patterns, and payment-method links. Collect additional operational data |
| 6 | **Use seasonal demand planning** | Prepare inventory, marketing, product availability, delivery and support capacity for peak months like December |
| 7 | **Manage customers by profitability** | Evaluate revenue, profit, margin, order frequency, average order value, and recency together |
| 8 | **Monitor payment method performance** | Track volume, sales, profit, margin, cancellation rate, and return rate per method |

---

## Skills Demonstrated

**Python & Analytics:** Pandas, NumPy, Data Cleaning, Data Validation, EDA, Customer Segmentation, RFM Analysis, Customer Profitability, CLV-style Analysis, Correlation Analysis

**SQL / PostgreSQL:** SELECT, WHERE, GROUP BY, ORDER BY, CASE, JOIN, CTE, Window Functions, NTILE, Aggregations, Ranking

**Power BI:** Data Modeling, Relationships, DAX Measures, KPI Cards, Bar / Column / Line / Donut / Scatter Charts, Dashboard Design, Business Performance Reporting

---

## Author

**Sabbir Hossain**
Aspiring Data Analyst | BI Engineer

Python | SQL | PostgreSQL | Power BI | Excel

- LinkedIn: [sabbir-hossain-2001da](https://www.linkedin.com/in/sabbir-hossain-2001da)
- GitHub: [SABBIR-HOSSAIN-001](https://github.com/SABBIR-HOSSAIN-001)f
