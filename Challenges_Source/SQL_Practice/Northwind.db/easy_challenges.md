# Easy challenges


**1) Show the category_name and description from the categories table sorted by category_name.**

```SQL
SELECT category_name, description
FROM categories
ORDER BY category_name;
```
___

**2) Show all the contact_name, address, city of all customers which are not from 'Germany', 'Mexico', 'Spain'**

```SQL
SELECT contact_name, address, city
FROM customers
WHERE country NOT IN ('Germany', 'Mexico', 'Spain');
```
___

**3) Show order_date, shipped_date, customer_id, Freight of all orders placed on 2018 Feb 26**

```SQL
SELECT order_date, shipped_date, customer_id, Freight
FROM orders
WHERE order_date = '2018-02-26';
```
___

**4) Show the employee_id, order_id, customer_id, required_date, shipped_date from all orders shipped later than the required date**

```SQL
SELECT 
    employee_id,
    order_id,
    customer_id,
    required_date,
    shipped_date
FROM 
   orders
WHERE
   required_date < shipped_date;

```
___

**5) Show all the even numbered Order_id from the orders table**

```SQL
SELECT order_id
FROM orders
WHERE order_id % 2 = 0;
```

**6) Show the city, company_name, contact_name of all customers from cities which contains the letter 'L' in the city name, sorted by contact_name**

```SQL
SELECT city, company_name, contact_name
FROM customers
WHERE city LIKE '%L%'
ORDER BY contact_name;
```
___

**7) Show the company_name, contact_name, fax number of all customers that has a fax number. (not null)**

```SQL
SELECT company_name, contact_name, fax
FROM customers
WHERE fax NOT NULL;
```
___

**8) Show the first_name, last_name. hire_date of the most recently hired employee.**

```SQL
SELECT TOP 1 first_name, last_name, hire_date
FROM employees
ORDER BY hire_date DESC;
```
___

**9) Show the average unit price rounded to 2 decimal places, the total units in stock, total discontinued products from the products table.**

```SQL
SELECT 
    ROUND(AVG(unit_price), 2),
    SUM(units_in_stock),
    SUM(discontinued)
FROM products;
```