# 10 - Dealing with indexes
___

**10.1) Create an index on the "Name" column to improve query performance.**

```SQL
CREATE INDEX idx_name ON Employees(Name);
```
___

**10.2) Write a SQL query to create an index on the last_name column in the employees table.**
```SQL
CREATE INDEX lastname_idx ON employees(last_name);
```
___

**10.3) Write a SQL query to improve query performance by creating an index on the product_name column in the products table.**
```SQL
CREATE INDEX product_name_idx ON products(product_name);
```
___

**10.4) Write a SQL query to create a composite index on the city and state columns in the addresses table.**
```SQL
CREATE INDEX composite_idx ON addresses(city, state)
```
___

**10.5) Write a SQL query to create an index on the email column in the users table.**
```SQL
CREATE INDEX mail_idx ON users(email)
```
**10.6) Remove the index "idx_Name" from the "Employees" table.**

```SQL
DROP INDEX idx_Name ON Employee
```
___

**10.7) Write a SQL query to remove the index named lastname_idx from the employees table.**
```SQL
DROP INDEX lastname_idx ON employee
```
___

**10.8) Write a SQL query to drop the index on the product_name column in the products table.**
```SQL
DROP INDEX product_name_idx ON products
```
___

**10.9) Write a SQL query to delete the composite index on the city and state columns in the addresses table.**
```SQL
DROP INDEX composite_idx ON addresses
```
___

**10.10) Write a SQL query to remove the index on the email column in the users table.**
```SQL
DROP INDEX mail_idx ON users
```
