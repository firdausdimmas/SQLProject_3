# Analyzing Motorcycle Part Sales

### Project Overview

![Motorcycle](https://github.com/user-attachments/assets/c5ebe9fe-c316-4425-800e-ced4f5bff7ca)

We're working for a company that sells motorcycle parts, and they've asked for some help in analyzing their sales data.

They operate three warehouses in the area, selling both retail and wholesale. They offer a variety of parts and accept credit cards, cash, and bank transfer as payment methods. However, each payment type incurs a different fee.

The board of directors wants to gain a better understanding of wholesale revenue by product line, and how this varies month-to-month and across warehouses. We have been tasked with calculating net revenue for each product line and grouping results by month and warehouse. The results should be filtered so that only `"Wholesale"` orders are included.

### Data Sources

This company have provided access to their database, which contains the following table called `sales`:

#### Sales

<table>
  <tr>
    <th>Column</th>
    <th>Data Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>order_number</code></td>
    <td>VARCHAR</td>
    <td>Unique order number.</td>
  </tr>
  <tr>
    <td><code>date</code></td>
    <td>DATE</td>
    <td>Date of the order, from June to August 2021.</td>
  </tr>
  <tr>
    <td><code>warehouse</code></td>
    <td>VARCHAR</td>
    <td>The warehouse where the order was made from — <strong>North</strong>, <strong>Central</strong>, or <strong>West</strong>.</td>
  </tr>
  <tr>
    <td><code>client_type</code></td>
    <td>VARCHAR</td>
    <td>Whether the order was <strong>Retail</strong> or <strong>Wholesale</strong>.</td>
  </tr>
  <tr>
    <td><code>product_line</code></td>
    <td>VARCHAR</td>
    <td>Type of product ordered.</td>
  </tr>
  <tr>
    <td><code>quantity</code></td>
    <td>INT</td>
    <td>Number of products ordered.</td>
  </tr>
  <tr>
    <td><code>unit_price</code></td>
    <td>FLOAT</td>
    <td>Price per product (dollars).</td>
  </tr>
  <tr>
    <td><code>total</code></td>
    <td>FLOAT</td>
    <td>Total price of the order (dollars).</td>
  </tr>
  <tr>
    <td><code>payment</code></td>
    <td>VARCHAR</td>
    <td>Payment method — <strong>Credit card</strong>, <strong>Transfer</strong>, or <strong>Cash</strong>.</td>
  </tr>
  <tr>
    <td><code>payment_fee</code></td>
    <td>FLOAT</td>
    <td>Percentage of <code>total</code> charged as a result of the <code>payment</code> method.</td>
  </tr>
</table>

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
