# Hard challenges


**1) Show the employee's first_name and last_name, a "num_orders" column with a count of the orders taken, and a column called "Shipped" that displays "On Time" if the order shipped_date is less or equal to the required_date, "Late" if the order shipped late, "Not Shipped" if shipped_date is null.**

**Order by employee last_name, then by first_name, and then descending by number of orders.**

```SQL
SELECT 
    e.first_name,
    e.last_name,
    COUNT(o.order_id) AS num_orders,
    (
    CASE
        WHEN o.shipped_date <= o.required_date THEN 'On Time'
        WHEN o.shipped_date > o.required_date THEN 'Late'
        ELSE 'Not Shipped'
    END AS Shipped
    )

FROM
    orders o

JOIN
    employees e
ON
    o.employee_id = e.employee_id

GROUP BY 
    e.first_name,
    e.last_name,
    (
    CASE
        WHEN o.shipped_date <= o.required_date THEN 'On Time'
        WHEN o.shipped_date > o.required_date THEN 'Late'
        ELSE 'Not Shipped'
    END
    )

ORDER BY 
    e.last_name,
    e.first_name,
    COUNT(o.order_id) DESC;
```
___

**2) Show how much money the company lost due to giving discounts each year, order the years from most recent to least recent. Round to 2 decimal places**

```SQL
SELECT 
  YEAR(o.order_date) AS year,
  ROUND(SUM(p.unit_price * od.quantity * od.discount), 2) AS total_discount_loss
FROM 
  orders o
JOIN 
  order_details od ON o.order_id = od.order_id
JOIN
  products p ON od.product_id = p.product_id
WHERE
  od.discount > 0
GROUP BY
  YEAR(o.order_date)
ORDER BY
  year DESC;
```