# 1 - Create table
___

**1.1) Create a table named "Employees" with columns for ID, Name, Age, and Salary.**

```SQL
CREATE TABLE Employees (
    ID INT PRIMARY KEY,
    Name VARCHAR(25),
    Age SMALLINT,
    Salary DECIMAL(8, 3) 
)
```
___

**1.2) Write a SQL query to create a table with three columns: id, name, and age. Add a primary key constraint on the id column.**
```SQL
CREATE TABLE table (
    tableID INT PRIMARY KEY,
    tableName VARCHAR(100),
    Age SMALLINT
)
```
___

**1.3) Write a SQL query to create a table with four columns: product_id, product_name, price, and quantity. Ensure that the price column cannot have negative values.**
```SQL
CREATE TABLE product (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(30) NOT NULL,
    price DECIMAL(10,2) CHECK (price >= 0), 
    quantity INT CHECK (quantity BETWEEN 1 AND 100)
)
```
___

**1.4) Write a SQL query to create a table with two columns: user_id and email. Make sure the email column only accepts unique values.**
```SQL
CREATE TABLE user (
    user_id INT PRIMARY KEY,
    email VARCHAR(15) UNIQUE
)
```
___

**1.5) Write a SQL query to create a table with five columns: order_id, customer_id, order_date, total_amount, and status. Add a NOT NULL constraint to the order_date column.**
```SQL
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE NOT NULL,
    total_amount INT,
    status VARCHAR(10) CHECK (status IN ('UNDER_REVIEW', 'CHECKED', 'SHIPPED', 'DONE')),
    FOREIGN KEY (customer_id) REFERENCES customer(customer_id)
);
```
