# 3 - Deleting records into table
___

**3.1) Delete the employee with EmployeeID = 4.**

```SQL
DELETE FROM employee
WHERE empID = 4;
```
___

**3.2) Write a SQL query to delete a single record from the 'customers' table where the deletion condition includes a subquery comparing aggregated values.**

> ⚠️ Note :- Group By `Not` use directly with delete 
```SQL
DELETE FROM customers
WHERE placeName IN (
    SELECT placeName
    FROM customers
    GROUP BY placeName
    HAVING SUM(spending) < 3000
);

```
___

**3.3) Write a SQL query to delete a single record from a table by joining it with another table to evaluate a complex deletion condition.**

```SQL
DELETE TOP (1) visitor
FROM 
    Visitors visitor
LEFT JOIN 
    places place
ON
    visitor.placeID = place.placeID
WHERE visitor.placeID IS NULL    
```
___

**3.4) Delete all employees with a salary less than 50000.**

```SQL
DELETE FROM employees
WHERE salary < 50000;
```
___

**3.5) Write a SQL query to delete all records from the 'students' table where the 'grade' is 'F'.**

```SQL
DELETE FROM students
WHERE grade = 'F;
```
___

**3.6) Write a SQL query to delete all records from the 'inventory' table where the 'quantity' is less than 10.**

```SQL
DELETE FROM inventory
WHERE quantity < 10;
```
___

**3.7) Write a SQL query to delete all records from the 'orders' table where the 'order_date' is older than two years.**

```SQL
DELETE FROM orders
WHERE order_date < DATEADD(YEAR, -2, GETDATE());
```
___

**3.8) Write a SQL query to delete all records from the 'products' table where the 'category' is 'Discontinued'.**

```SQL
DELETE FROM products
WHERE Discontinued < 10;
```
___

**3.9) Write a SQL query to delete records from the `employees` table where the `department_id` matches a subquery that identifies closed departments.**

```SQL
DELETE FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE dep_state = 'Closed'
);
```
___

**3.10) Delete all records from the "Employees" table.**

```SQL
DELETE FROM Employees;
```
___

**3.11) Write a SQL query to delete records from the `orders` table where the `customer_id` matches inactive customers in the `customers` table.**

```SQL
DELETE o
FROM orders o
JOIN customers c
ON o.customer_id = c.customer_id
WHERE c.customer_state = 'inactive' 
```