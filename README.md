# Maven-Toys-Analysis
 
Analysis based off Sales & inventory data for a fictitious chain of toy stores in Mexico called Maven Toys, including information about products, stores, daily sales transactions, and current inventory levels at each location.

![]()

## Problem statement
- Which product categories drive the biggest profits? Is this the same across store locations?
- How much money is tied up in inventory at the toy stores? How long will it last?
- Are sales being lost with out-of-stock products at certain locations?

## Solution

```
--QUESTION 1
--Query to Calculate total profits per product category across all store locations.

SELECT p.product_category, SUM((p.product_price - p.product_cost) * s.Units) AS total_profit
FROM sales AS s
JOIN products p ON s.product_id = p.product_id
GROUP BY p.product_category
ORDER BY total_profit DESC;

---Query to Calculate total profits per product category for each store location.

SELECT st.store_location, p.product_category, SUM((p.product_price - p.product_cost) * s.units) AS total_profit
FROM sales AS S
JOIN products p ON s.product_id = p.product_id
JOIN stores AS st ON s.store_id = st.store_id
GROUP BY st.store_location, p.product_Category
ORDER BY st.store_location, total_profit DESC;


--QUESTION 2
---Query to Calculate the total value of inventory across all toy stores.

SELECT SUM(p.product_cost * i.stock_on_hand) AS total_inventory_value
FROM products p
JOIN inventory i ON p.product_id = i.product_id;


--QUESTION 3
--Query to Identify out-of-stock products and potential lost sales at each location.

SELECT st.store_location, p.product_name, s.units AS units_sold, i.stock_on_hand
FROM sales AS s
JOIN products p ON s.Product_ID = p.Product_ID
JOIN stores AS st ON s.store_id = st.store_id
JOIN inventory i ON s.store_id = i.store_id AND s.product_id = i.product_id
WHERE i.stock_on_hand = 0;










```
