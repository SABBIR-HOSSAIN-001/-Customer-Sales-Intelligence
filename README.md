# Customer Sales Intelligence

End-to-end customer sales analytics project using **Python, PostgreSQL and Power BI**: RFM segmentation, customer profitability, discount analysis, and business recommendations.

![Dashboard Preview](images/01_executive_overview.png)

## Headline Findings

| Metric | Value |
| --- | --- |
| Total Sales | 609.53M `<currency>` |
| Total Profit | 84.98M (13.94% margin) |
| Orders / Customers | 10,000 / 1,498 |
| Delivered / Cancelled / Returned | 91.20% / 4.96% / 3.84% |

1. **Revenue is concentrated.** The top customer-value tercile (High Value) generates 59.6% of sales, so retention matters most there.
2. **Big customers are not the most profitable.** High Value customers have the *lowest* margin (13.28%), against 16.36% for Low Value.
3. **At-Risk customers are worth winning back.** 267 customers have generated 129.82M in historical sales but show weak recent activity.
4. **Sales volume does not equal profit.** PROD-018 has 26.29M in sales at an 8.16% margin. PROD-054 has 23.40M at 17.05%.
5. **Discounts show no clear payoff.** Correlation with sales is -0.055 and with profit is -0.065, which is weak and not causal.

## Workflow

`Python (clean, EDA, RFM)` → `PostgreSQL (SQL analysis)` → `Power BI (4-page dashboard)` → `Insights & recommendations`

## Repository Contents

```
├── images/                                      # dashboard screenshots
├── Customer_Sales_Intelligence--python.ipynb    # cleaning, EDA, RFM, profitability
├── Customers_Sales_Intelligence__sql.query.sql  # PostgreSQL analysis
├── Customer_Sales_Intelligence-BI.pbix          # Power BI dashboard
├── Customer_Sales_Intelligence_cleaned.xlsx     # cleaned dataset
├── RFM_Customer_Segments.csv                    # RFM output
└── README.md
```

## Data

- **Source:** `<TODO: Kaggle link / synthetic / company data>`
- **Size:** 10,000 orders, 1,498 customers
- **Currency:** `<TODO: e.g. BDT>`
- **Data model:** `Orders` (fact table) linked to `Customers` (with Region), `Products` (with Category) and the RFM segment table.
- **Order columns:** Order_ID, Order_Date, Customer_ID, Product_ID, Quantity, Discount, Sales, Profit, Payment_Method, Order_Status

**Cleaning notes**
- Checked types, missing values, duplicates, unique Order_ID, and business rules (quantity, discount, sales, profit).
- Undefined payment methods were labelled `Unknown` instead of dropped.
- Cancelled and returned orders have zero sales and profit in the data, so they are treated as operational outcomes. No financial loss is assumed.

## Methodology

**Customer value segments.** Customers are split into three equal groups (`NTILE(3)`) by total sales: Low, Medium, High.

| Segment | Customers | Orders | Sales | Margin |
| --- | --- | --- | --- | --- |
| Low Value | 500 | 2,472 | 67.86M | 16.36% |
| Medium Value | 499 | 3,451 | 178.56M | 14.38% |
| High Value | 499 | 4,077 | 363.11M | 13.28% |

> Because these are equal-sized groups by design, the 59.6% share reflects how concentrated sales are among the top third of customers. It is not a discovered threshold.

**RFM segments.**
`<TODO: describe scoring, e.g. R/F/M scored 1-5 with NTILE(5), and the rule for each segment. Example: Champions = R>=4 and F>=4, At Risk = R<=2 and F>=3 ...>`

| Segment | Customers | Orders | Historical Sales |
| --- | --- | --- | --- |
| Loyal | 444 | 3,522 | 192.59M |
| Champions | 188 | 1,821 | 136.95M |
| At Risk | 267 | 2,113 | 129.82M |
| Lost | 323 | 1,337 | 75.55M |
| New | 170 | 751 | 47.72M |
| Potential | 106 | 456 | 26.91M |

**Correlations (PostgreSQL):** Sales vs Profit 0.9466, Discount vs Sales -0.0552, Discount vs Profit -0.0645.

## Power BI Dashboard

A 4-page interactive dashboard built in Power BI.

### 1. Executive Overview
KPIs, monthly sales trend, sales vs profit, order status mix and regional sales.

![Executive Overview](images/01_executive_overview.png)

### 2. Product Performance
Top products by sales and profit, margin by product, quantity vs sales.

![Product Performance](images/02_product_performance.png)

### 3. Customer Intelligence
Top customers, RFM segments and customer value segments.

![Customer Intelligence](images/03_customer_intelligence.png)

### 4. Business Performance
Payment methods, order status, discount impact and monthly margin.

![Business Performance](images/04_business_performance.png)

## More Insights

- **Seasonality:** December is the strongest month (59.08M sales, 8.20M profit). February is the weakest (43.00M). The largest month-over-month jumps were March (+19.34%), December (+18.26%) and July (+11.37%).
- **Payments:** bKash has the highest volume and sales. Card users have the highest margin (14.03%).
- **Fulfilment:** About 8.8% of orders were cancelled or returned. Cost data would be needed to size the financial impact.

## Recommendations

1. **Protect High Value customers** with loyalty benefits and repeat-purchase campaigns, and investigate why their margin is lower.
2. **Run reactivation campaigns** for the 267 At-Risk customers.
3. **Review low-margin, high-sales products** for pricing, supplier cost, and discount level.
4. **Replace blanket discounts with targeted ones** based on segment and product margin.
5. **Investigate cancellations and returns** by product, customer, payment method, and delivery.
6. **Plan inventory and support capacity** ahead of peak months such as December.
7. **Rank customers by profit and margin as well as revenue.**

## Limitations

- Correlation does not show causation.
- Seasonal patterns come from a single year of data. `<TODO: adjust if the data is synthetic>`
- No cost, return-reason, or campaign data, so recommendations are directional.

## Skills Demonstrated

**Python:** Pandas, NumPy, Matplotlib, data validation, EDA, RFM, profitability analysis
**SQL (PostgreSQL):** aggregations, CASE, CTEs, JOINs, window functions, NTILE, ranking, correlation
**Power BI:** data modeling, DAX measures, KPI cards, multi-page dashboard design

## Author

**Sabbir Hossain**, aspiring Data Analyst | BI Engineer
Python · SQL · PostgreSQL · Power BI · Excel
