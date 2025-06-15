# 2 - Add new column
___

**2.1) Add a new column "Department" to the "Employees" table.**

```SQL
ALTER TABLE Employees
ADD Department VARCHAR(25)

ALTER TABLE Employees
ADD CONSTRAINT dep_fk
FOREIGN KEY (Department) REFERENCES Department(dep_name)
```
___

**2.2) Write a SQL query to add a new column named phone_number to an existing table called customers**
```SQL
ALTER TABLE customers
ADD phone_number INT
```
___

**2.3) Write a SQL query to add a new column named created_at with a default value of the current timestamp to a table named orders.**
```SQL
ALTER TABLE orders
ADD created_at DATETIME DEFAULT GETDATE()
```
___

**2.4) Write a SQL query to add a new column named is_active with a BOOLEAN data type to a table named users.**
```SQL
ALTER TABLE users
ADD is_active BIT  -- Bit is 0 or 1 with default 0
```
___

**2.5) Write a SQL query to add a new column named discount_rate with a DECIMAL data type to a table named products.**
```SQL
ALTER TABLE products
ADD discount_rate DECIMAL(8,2)
```
