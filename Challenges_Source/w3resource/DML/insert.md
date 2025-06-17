# 1 - Inserting records into table
___

**1.1) Insert a new employee record into the "Employees" table.**

```SQL
INSERT INTO Employees (empID, FName, LName, DepName, Salary)
VALUES ('empID', 'FName', 'LName', 'DepName', 'Salary');
```
___

**1.2) Write a SQL query to insert a single record into the 'employees' table where one column's value is determined by a subquery that selects the highest salary from the 'salaries' table.**

```SQL
INSERT INTO employees (empID, FName, LName, DepName, Salary)
VALUES (
    'empID',
    'FName', 
    'LName', 
    'DepName',
    (SELECT TOP 1 salary FROM salaries ORDER BY salary DESC)
);
```
___

**1.3) Write a SQL query to insert a single record into the 'products' table with one column computed by an arithmetic expression based on another column’s value.**

```SQL
INSERT INTO products (productID, productName, salary, delivery, totalCost)
VALUES (
    'productID',
    'productName',
    'salary',
    'delivery'
    salary + delivery
);
```
___

**1.4) Write a SQL query to insert a single record into a table with default constraints, explicitly providing values only for non-default columns.**

```SQL
-- employees table (empID, FName, LName, DepName, Salary)
INSERT INTO employees (empID, FName, LName, DepName)
VALUES (
    'empID',
    'FName', 
    'LName', 
    'DepName'
);
```
___

**1.5) Write a SQL query to insert a single record into the 'orders' table using a CASE expression to conditionally determine one column's value.**

```SQL
DECLARE @amount DECIMAL(10, 2) = 800;

INSERT INTO orders (orderID, customerName, amount, status)
VALUES (
    102,
    'Omar Mohamed',
    @amount,
    CASE 
        WHEN @amount >= 1000 THEN 'VIP'
        ELSE 'Regular'
    END
);
```

**1.6) Insert multiple employee records into the "Employees" table.**

```SQL
INSERT INTO Employees (empID, FName, LName, DepName, Salary)
VALUES
    ('empID', 'FName', 'LName', 'DepName', 'Salary'),
    ('empID2', 'FName2', 'LName2', 'DepName2', 'Salary2');

```
___

**1.7) Write a SQL query to insert multiple records into the 'inventory' table mixing explicit values with columns that rely on default constraints.**

```SQL
-- inventory (item_id, item_name, quantity, category, created_at)
INSERT INTO inventory (item_id, item_name)
VALUES
   ('item_id1', 'item_name1'),
   ('item_id2', 'item_name2'),
   ('item_id3', 'item_name3');
```
___

**1.8) Write a SQL query to insert multiple records into a table using a SELECT statement from another table with filtering and transformation conditions.**
```SQL
INSERT INTO old_employees (id, name, updated_salary)
SELECT 
    id, 
    name, 
    salary * 1.10
FROM 
    employees
WHERE 
    age > 50;
```
___

**1.9) Write a SQL query to copy all active employees from the `employees` table into the `active_employees` table.**

```SQL
INSERT INTO active_employees (id, name, age)
SELECT 
    id, 
    name, 
    age
FROM 
    employees
WHERE 
    state = 'active';
```
___

**1.10) Write a SQL query to copy all products with a price greater than 100 from the `products` table into the `premium_products` table.**

```SQL
INSERT INTO premium_products (product_id, product_name, price)
SELECT 
    product_id, 
    product_name,
    price
FROM 
    products
WHERE 
    price > 100;
```

___

**1.11) Write a SQL query to copy all orders from the `orders` table placed in the last month into the `recent_orders` table.**

```SQL
INSERT INTO recent_orders (order_id, order_name, direction, order_data)
SELECT
    order_id,
    order_name,
    direction,
    order_data
FROM
    orders
WHERE
    MONTH(order_data) = MONTH(DATEADD(MONTH, -1, GETDATE()));
```
