# Analyzing Motorcycle Part Sales

### Project Overview

We're working for a company that sells motorcycle parts, and they've asked for some help in analyzing their sales data!

They operate three warehouses in the area, selling both retail and wholesale. They offer a variety of parts and accept credit cards, cash, and bank transfer as payment methods. However, each payment type incurs a different fee.

The board of directors wants to gain a better understanding of wholesale revenue by product line, and how this varies month-to-month and across warehouses. You have been tasked with calculating net revenue for each product line and grouping results by month and warehouse. The results should be filtered so that only `"Wholesale"` orders are included.

### Data Sources

This company have provided access to their database, which contains the following table called `sales`:

#### Sales
| Column | Data type | Description |
|--------|-----------|-------------|
| `order_number` | `VARCHAR` | Unique order number. |
| `date` | `DATE` | Date of the order, from June to August 2021. |
| `warehouse` | `VARCHAR` | The warehouse that the order was made from&mdash; `North`, `Central`, or `West`. |
| `client_type` | `VARCHAR` | Whether the order was `Retail` or `Wholesale`. |
| `product_line` | `VARCHAR` | Type of product ordered. |
| `quantity` | `INT` | Number of products ordered. | 
| `unit_price` | `FLOAT` | Price per product (dollars). |
| `total` | `FLOAT` | Total price of the order (dollars). |
| `payment` | `VARCHAR` | Payment method&mdash;`Credit card`, `Transfer`, or `Cash`. |
| `payment_fee` | `FLOAT` | Percentage of `total` charged as a result of the `payment` method. |

### Exploratory Data Analysis (EDA)

EDA involved exploring the sales data to answer key questions, such as:

- Which product lines generate the highest net revenue in wholesale?
- Are there significant differences in net revenue between the three warehouses?
- Which months show the highest or lowest wholesale revenue — is there any seasonality?

### Data Analysis

Include some interesting code/features worked with

```sql
-- Wholesale Net Revenue Generated per Product Line
SELECT product_line,
	   to_char(date, 'Month') AS month,
	   warehouse,
	   SUM(total - payment_fee) AS net_revenue
FROM sales
WHERE client_type = 'Wholesale'
GROUP BY product_line, warehouse, month
ORDER BY product_line, month, net_revenue DESC;
```

### Results/Findings

The analysis results are summarized as follows:
1. Engine Parts and Frame & Body consistently generate the highest wholesale net revenue across all warehouses.
2. Central Warehouse leads in revenue for most product lines, while West Warehouse has the lowest contribution, especially in July.
3. Revenue has shown a strong upward trend from June through August.

### Recommendations

Based on the analysis, we recommend the following actions:
- Consider expanding the product range, offering bundled deals, or promotions around the top revenue generator products to further capitalize on their strong demand..
- Investigate why West Warehouse underperforms, particularly in July. Review factors such as inventory availability, local demand, staffing, and logistics challenges.
- With a strong upward trend from June to August, consider scaling operations by increasing stock levels, expanding marketing efforts, or offering volume discounts for wholesale customers.
