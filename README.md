# Customer Sales Intelligence

## 📊 Project Overview

**Customer Sales Intelligence** is an end-to-end data analytics and business intelligence project designed to analyze customer behavior, sales performance, profitability, product performance, and business operations.

The project combines **Python, PostgreSQL, and Power BI** to transform raw transactional data into actionable business insights and recommendations.

The complete workflow follows:

**Python → PostgreSQL → Power BI → Business Insights → Business Recommendations**

The main objective of this project is to understand:

- How the business is performing overall
- Which products generate the most sales and profit
- Which customers contribute the most revenue
- Which customers are at risk of becoming inactive
- How customer value differs across segments
- How discounts affect sales and profitability
- Which payment methods perform better
- How order cancellations and returns affect operations
- How sales and profitability change over time
- Where the business can improve revenue, profitability, and customer retention

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| Python | Data cleaning, analysis, customer segmentation, RFM analysis |
| Pandas | Data manipulation and analysis |
| NumPy | Numerical calculations |
| Matplotlib | Data visualization and exploratory analysis |
| PostgreSQL | SQL-based business analysis |
| pgAdmin | PostgreSQL database management |
| Power BI | Interactive dashboards and business intelligence |
| Excel | Initial data inspection and validation |
| GitHub | Project documentation and portfolio presentation |

---

## 📁 Project Structure

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
├── Data/
│   └── Customer_Sales_Intelligence_cleaned.xlsx
│
└── README.md
```

---

## 📌 Dataset Overview

The project uses an e-commerce transactional dataset containing **10,000 orders** and approximately **1,500 customers**.

The main order-level dataset contains the following fields:

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

## 🔎 Data Preparation & Quality Validation

Before performing business analysis, the dataset was validated and cleaned.

The following checks were performed:

- Data type validation
- Missing value detection
- Duplicate detection
- Unique Order ID validation
- Quantity validation
- Discount validation
- Sales validation
- Profit validation
- Payment method validation
- Order status validation
- Business-rule validation

### Data Quality Findings

The dataset contained a small number of undefined payment methods. Instead of deleting these records, undefined payment methods were categorized as **Unknown**. This preserves the original transactions while making the dataset suitable for analysis.

The analysis also identified that cancelled and returned orders have zero recorded sales and profit in the dataset. Therefore, they were treated as operational outcomes rather than assuming direct financial losses that are not explicitly recorded.

---

## 🐍 Python Analysis

Python was used as the main analytical environment for exploratory analysis, customer analytics, segmentation, and business intelligence preparation.

### 1. Overall Business KPIs

- Total Orders
- Total Customers
- Total Sales
- Total Profit
- Average Order Value
- Profit Margin
- Delivery Rate
- Cancellation Rate
- Return Rate

### 2. Monthly Sales Analysis

- Monthly Sales
- Monthly Profit
- Monthly Orders
- Profit Margin
- Month-over-Month Sales Growth

This helped identify seasonal patterns and high/low-performing periods.

### 3. Product Performance Analysis

- Sales
- Profit
- Profit Margin
- Quantity
- Product ranking

This analysis demonstrated that high sales volume does not always result in high profitability.

### 4. Customer Analysis

- Total Sales
- Total Profit
- Order Frequency
- Average Order Value
- Profit Margin

This helped identify high-value customers and customers generating relatively low margins despite high revenue.

---

## 👥 Customer Segmentation

Customers were segmented based on their purchasing behavior and monetary contribution into three customer value groups: **Low Value**, **Medium Value**, and **High Value**.

### Customer Value Results

| Segment | Customers | Orders | Sales | Profit Margin |
|---------|-----------|--------|-------|---------------|
| Low Value | 500 | 2,472 | 67.86M | 16.36% |
| Medium Value | 499 | 3,451 | 178.56M | 14.38% |
| High Value | 499 | 4,077 | 363.11M | 13.28% |

High-value customers generated approximately **59.6% of total sales**. This indicates that a relatively small portion of the customer base contributes a significant share of business revenue.

---

## 📈 RFM Analysis

RFM analysis was performed to understand customer engagement and purchasing behavior.

- **Recency** — How recently the customer purchased
- **Frequency** — How often the customer purchased
- **Monetary** — How much the customer spent

Customers were categorized into: Champions, Loyal Customers, At Risk, Lost Customers, New Customers, and Potential Customers.

### RFM Results

| Segment | Customers | Orders | Historical Sales |
|---------|-----------|--------|------------------|
| Loyal Customers | 444 | 3,522 | 192.59M |
| Champions | 188 | 1,821 | 136.95M |
| At Risk | 267 | 2,113 | 129.82M |
| Lost Customers | 323 | 1,337 | 75.55M |
| New Customers | 170 | 751 | 47.72M |
| Potential Customers | 106 | 456 | 26.91M |

The analysis shows that Loyal Customers represent the largest RFM segment by customer count and historical sales.

The At Risk segment is also important because these customers have previously generated approximately 129.82M in sales, making them a meaningful retention opportunity.

---

## 💰 Customer Profitability Analysis

Customer profitability was analyzed instead of relying only on revenue.

This analysis showed that **high revenue does not always mean high profitability**. For example, some customers generated more than 1M in sales but had profit margins around 10–12%, while some lower-revenue customers achieved considerably higher margins.

This highlights the importance of evaluating customers using both **Revenue + Profitability**.

---

## 🧮 CLV-Style Analysis

A simplified Customer Lifetime Value-style analysis was performed using:

- Total Customer Sales
- Total Customer Profit
- Number of Orders
- Average Order Value
- Customer Profit Margin

This approach helps identify customers who provide stronger long-term business value.

---

## 🗄️ PostgreSQL Analysis

The cleaned order dataset was imported into PostgreSQL for SQL-based business analysis.

A relational table was created:

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

SQL analysis included:

- Monthly sales analysis
- Month-over-Month growth
- Product ranking
- Customer ranking
- Customer frequency
- RFM analysis
- Customer value segmentation
- Customer profitability
- Payment method analysis
- Order status analysis
- Discount analysis
- Correlation analysis
- Window functions
- NTILE segmentation
- Aggregation and conditional logic

---

## 📊 Correlation Analysis

The following correlations were calculated in PostgreSQL:

| Relationship | Correlation |
|--------------|-------------|
| Sales vs Profit | 0.9466 |
| Discount vs Sales | -0.0552 |
| Discount vs Profit | -0.0645 |

### Interpretation

There is a strong positive relationship between sales and profit. However, the relationship between discount and sales/profit is weakly negative.

This does not prove that discounts cause lower sales or profit. Correlation indicates association, not causation.

---

## 📊 Power BI Dashboard

The cleaned and analyzed data was visualized in Power BI through four analytical pages.

### Page 1 — Executive Overview

- Total Sales
- Total Profit
- Profit Margin
- Total Orders
- Total Customers
- Monthly Sales Trend
- Sales vs Profit
- Order Status
- Region-wise Sales

**Purpose:** Provides a high-level overview of overall business performance.

### Page 2 — Product Performance

- Top 10 Products by Sales
- Top 10 Products by Profit
- Category Performance
- Product Profit Margin
- Quantity vs Sales

**Purpose:** Identifies high-revenue products, high-profit products, high-margin products, and products where sales and profitability differ.

### Page 3 — Customer Intelligence

- Top 10 Customers by Sales
- RFM Segment Count
- RFM Segment-wise Sales
- Customer Value Segment Count
- Customer Value Segment-wise Sales

**Purpose:** Helps understand customer contribution, customer value, customer loyalty, retention opportunities, high-value customer groups, and at-risk customers.

### Page 4 — Business Performance

- Payment Method Analysis
- Order Status Analysis
- Discount Analysis
- Monthly Profit Margin
- Executive KPI Cards

**Purpose:** Focuses on operational and financial performance, including payment behavior, order fulfillment issues, discount patterns, profitability trends, and operational improvement opportunities.

---

## 📌 Key Business Insights

### 1. Overall Business Performance

| Metric | Value |
|--------|-------|
| Total Sales | 609.53M |
| Total Profit | 84.98M |
| Profit Margin | 13.94% |
| Total Orders | 10,000 |
| Total Customers | 1,498 |
| Average Order Value | 60,952.82 |

The overall delivery rate was 91.20%, while cancellation and return rates were 4.96% and 3.84% respectively.

### 2. December Was the Strongest Sales Month

December generated approximately **59.08M in sales** and **8.20M in profit**, making it the strongest monthly sales period in the dataset. February recorded the lowest monthly sales at approximately **43.00M**.

### 3. Sales Growth Was Uneven Throughout the Year

The strongest month-over-month increases included:

- March: +19.34%
- December: +18.26%
- July: +11.37%

This indicates that sales performance varies significantly throughout the year.

### 4. High Sales Do Not Always Mean High Profitability

| Product | Sales | Profit Margin |
|---------|-------|---------------|
| PROD-018 | 26.29M | 8.16% |
| PROD-054 | 23.40M | 17.05% |

This demonstrates why product decisions should consider profitability in addition to revenue.

### 5. High-Value Customers Drive a Large Share of Revenue

High-value customers generated approximately **363.11M in sales**, which represents around **59.6% of total sales**. This makes customer retention particularly important for revenue stability.

### 6. At-Risk Customers Represent a Significant Opportunity

The At-Risk RFM segment contains **267 customers** with approximately **129.82M historical sales**. These customers have previously contributed significant revenue but show weaker recent engagement, making them a potential customer-retention opportunity.

### 7. Loyal Customers Are the Largest RFM Segment

Loyal Customers represent **444 customers** and approximately **192.59M historical sales**. This indicates a substantial base of repeat customers that can be targeted for retention and cross-selling.

### 8. Customer Revenue and Customer Profitability Are Different

Several high-sales customers have relatively low profit margins. Therefore, customer management should not be based only on revenue.

The business should evaluate: **Customer Revenue + Customer Profit + Customer Margin + Purchase Frequency**

### 9. Payment Method Performance Differs

bKash generated the highest transaction volume and sales contribution among payment methods. Card users achieved the highest observed profit margin at approximately **14.03%**.

This suggests that payment-method performance should be monitored using both transaction volume and profitability.

### 10. Order Fulfillment Needs Monitoring

- Delivered: 91.20%
- Cancelled: 4.96%
- Returned: 3.84%

Approximately 8.8% of orders were not delivered successfully. The dataset records zero sales and profit for cancelled and returned orders, so direct financial loss should not be assumed without additional cost data.

### 11. Discounts Are Not Consistently Improving Performance

- Discount vs Sales: -0.0552
- Discount vs Profit: -0.0645

These are weak negative relationships. Increasing discounts does not automatically guarantee stronger sales or profitability, so discount strategies should be targeted rather than applied broadly.

---

## 💡 Business Recommendations

### 1. Prioritize High-Value Customer Retention

High-value customers generate approximately 59.6% of total sales. The business should prioritize:

- Personalized offers
- Loyalty benefits
- Early access to products
- Repeat-purchase campaigns
- Personalized product recommendations

### 2. Launch Reactivation Campaigns for At-Risk Customers

The At-Risk segment generated significant historical revenue. Recommended actions:

- Personalized reactivation emails
- Targeted offers
- Limited-time incentives
- Product recommendations based on previous purchases
- Reminder campaigns

The goal should be to move At-Risk customers back into the Loyal or Champion segments.

### 3. Optimize Product Profitability

Products should be evaluated using **Sales + Profit + Profit Margin**. High-sales but low-margin products should be reviewed for:

- Pricing
- Supplier cost
- Discount level
- Operational cost
- Product positioning

The objective should be to improve profitability without unnecessarily reducing sales volume.

### 4. Replace Blanket Discounts with Targeted Discounts

Instead of giving discounts to every customer, discounts should be targeted based on:

- Customer segment
- RFM segment
- Purchase history
- Product margin
- Customer profitability

High-margin products can support promotional campaigns more safely than low-margin products.

### 5. Improve Cancellation and Return Management

Approximately 8.8% of orders were cancelled or returned. The business should investigate:

- Reasons for cancellation
- Reasons for returns
- Product-level return patterns
- Delivery issues
- Customer-level patterns
- Payment-method-related issues

Additional operational data would help quantify the financial impact more accurately.

### 6. Use Seasonal Demand Planning

December was the strongest sales month. The business should prepare for high-demand periods through:

- Inventory planning
- Marketing campaigns
- Product availability
- Delivery capacity
- Customer support capacity

Historical monthly trends can be used to improve future demand planning.

### 7. Manage Customers Based on Profitability

Revenue alone should not determine customer priority. Customers should be evaluated using:

- Revenue
- Profit
- Profit Margin
- Order Frequency
- Average Order Value
- Recency

This can help identify customers who generate high revenue but relatively low profit.

### 8. Monitor Payment Method Performance

Payment methods should be monitored using:

- Transaction volume
- Sales
- Profit
- Profit Margin
- Cancellation rate
- Return rate

This can help the business understand not only which payment methods are popular, but also which ones are associated with stronger business performance.

---

## 🎯 Business Impact

This project demonstrates how raw transactional data can be transformed into a complete business intelligence workflow.

The analysis helps answer practical business questions such as:

- Which customers generate the most value?
- Which customers are at risk?
- Which products generate revenue versus profit?
- When does the business perform best?
- Are discounts improving performance?
- Which payment methods perform better?
- Where are operational problems occurring?
- How can the business improve customer retention and profitability?

---

## 📈 Key Takeaways

1. High revenue does not always mean high profitability.
2. High-value customers contribute a significant share of total revenue.
3. At-Risk customers represent an important retention opportunity.
4. Loyal customers form a strong base for repeat business.
5. Product-level profitability should be monitored alongside sales.
6. Discounts should be targeted instead of broadly applied.
7. Cancellation and return rates require operational attention.
8. Seasonal sales patterns can support better demand planning.
9. Customer profitability is more informative than revenue alone.
10. Data-driven segmentation can support more personalized business decisions.

---

## 🚀 Skills Demonstrated

**Python & Analytics**
- Python, Pandas, NumPy
- Data Cleaning, Data Validation
- Exploratory Data Analysis
- Customer Segmentation, RFM Analysis
- Customer Profitability, CLV-style Analysis
- Correlation Analysis

**SQL / PostgreSQL**
- SELECT, WHERE, GROUP BY, ORDER BY
- CASE, JOIN, CTE
- Window Functions, NTILE
- Aggregations, Ranking
- RFM Analysis, Correlation Analysis

**Power BI**
- Data Modeling, Relationships
- DAX Measures, KPI Cards
- Bar, Column, Line, Donut, and Scatter Charts
- Dashboard Design
- Customer Intelligence
- Business Performance Reporting

---

## 🧠 Analytical Workflow

```text
Raw Data
   ↓
Data Cleaning
   ↓
Data Quality Validation
   ↓
Exploratory Data Analysis
   ↓
Sales Performance Analysis
   ↓
Monthly Sales Analysis
   ↓
Product Performance
   ↓
Customer Analysis
   ↓
Customer Segmentation
   ↓
RFM Analysis
   ↓
RFM Customer Segmentation
   ↓
Customer Profitability
   ↓
CLV-style Analysis
   ↓
Payment Method Analysis
   ↓
Order Status Analysis
   ↓
Discount Analysis
   ↓
Correlation Analysis
   ↓
PostgreSQL Business Analysis
   ↓
Power BI Dashboard
   ↓
Business Insights
   ↓
Business Recommendations
```

---

## 📊 Project Outcome

This project demonstrates an end-to-end approach to solving business problems using data.

Instead of focusing only on descriptive statistics, the project connects:

**Data → Analysis → Visualization → Business Insight → Business Action**

The final objective is to support better decisions around:

- Customer retention
- Product profitability
- Pricing
- Discounts
- Sales planning
- Operational performance
- Customer value management

---

## 👤 Author

**Sabbir Hossain**

Aspiring Data Analyst | BI Engineer

Interested in transforming business data into meaningful insights using:

**Python | SQL | PostgreSQL | Power BI | Excel**

---

## ⭐ Project Highlights

- 10,000+ transactions analyzed
- 1,498 customers analyzed
- 609M+ total sales
- 84M+ total profit
- RFM customer segmentation
- Customer value segmentation
- Customer profitability analysis
- PostgreSQL business analysis
- Interactive Power BI dashboards
- Business recommendations based on analytical findings
