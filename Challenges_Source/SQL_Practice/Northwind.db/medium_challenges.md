# Medium challenges


**1) Show the ProductName, CompanyName, CategoryName from the products, suppliers, and categories table**

```SQL
SELECT product_name, company_name, category_name
FROM products
JOIN suppliers
   ON products.supplier_id = suppliers.supplier_id
join categories
   ON products.category_id = categories.category_id;
```
___

**2) Show the category_name and the average product unit price for each category rounded to 2 decimal places.**

```SQL
SELECT category_name, ROUND(AVG(unit_price), 2)
FROM categories
JOIN products
ON categories.category_id = products.category_id
GROUP BY products.category_id;
```
___

**3) Show the city, company_name, contact_name from the customers and suppliers table merged together.**

**Create a column which contains 'customers' or 'suppliers' depending on the table it came from.**

```SQL
SELECT 
    city,
    company_name,
    contact_name,
    'customers' AS came_from
FROM customers

UNION ALL

SELECT 
    city,
    company_name,
    contact_name,
    'suppliers' AS came_from
FROM suppliers;
```
___

**4) Show the total amount of orders for each year/month.**

```SQL
SELECT 
   YEAR(order_date) AS years,
   MONTH(order_date) AS monthes,
   COUNT(order_id) AS total_orders
FROM 
   orders
GROUP BY 
   YEAR(order_date),
   MONTH(order_date);

```