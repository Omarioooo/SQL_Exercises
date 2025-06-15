# 3 - Modify columns
___

**3.1) Change the data type of the "Salary" column to INTEGER.**

```SQL
ALTER TABLE Employees
ALTER COLUMN Salary INT;
```
___

**3.2) Write a SQL query to change the data type of the salary column in the employees table from INTEGER to DECIMAL(10, 2).**
```SQL
ALTER TABLE employees
ALTER COLUMN salary DECIMAL(10, 2)
```
___

**3.3) Write a SQL query to modify the description column in the products table to allow longer text by changing its data type to TEXT.**
```SQL
ALTER TABLE products
ALTER COLUMN DESCRIPTION TEXT
```
___

**3.4) Write a SQL query to change the data type of the date_of_birth column in the users table from DATE to DATETIME.**
```SQL
ALTER TABLE users
ALTER COLUMN DATETIME
```
___

**3.5) Write a SQL query to modify the quantity column in the inventory table from SMALLINT to INT.**
```SQL
ALTER TABLE inventory
ALTER quantity INT
```
