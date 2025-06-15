# 5 - Add constraints
___

**5.1) Add a unique constraint to the "Name" column to ensure no duplicate names.**

```SQL
ALTER TABLE tableName
ADD CONSTRAINT unique_name UNIQUE (Name)
```
___

**5.2) Write a SQL query to add a unique constraint to the username column in the users table.**
```SQL
ALTER TABLE users
ADD CONSTRAINT unique_user UNIQUE (username)
```
___

**5.3) Write a SQL query to ensure that the product_code column in the products table contains only unique values.**
```SQL
ALTER TABLE products
ADD CONSTRAINT unq_code UNIQUE (product_code)
```
___

**5.4) Write a SQL query to add a unique constraint to the email_address column in the customers table.**
```SQL
ALTER TABLE customers
ADD CONSTRAINT unq_mail UNIQUE (email_address)
```
___

**5.5) Write a SQL query to enforce uniqueness on the order_reference column in the orders table.**
```SQL
ALTER TABLE orders
ADD CONSTRAINT unq_order_ref UNIQUE (order_reference)
```

**5.6) Create a new table "Departments" and link it to "Employees" using a foreign key.**

```SQL
CREATE TABLE Departments (
    depID INT PRIMARY KEY,
    depName VARCHAR(25) NOT NULL,
    MangerID INT,
    FOREIGN KEY MangerID REFERENCES Employees(empID) 
)
```
___

**5.7) Write a SQL query to create a foreign key relationship between the customer_id column in the orders table and the id column in the customers table.**
```SQL
ALTER TABLE orders
ADD CONSTRAINT customerID_fk
FOREIGN KEY (customer_id)
REFERENCES customers(id)
```
___

**5.8) Write a SQL query to establish a foreign key constraint between the department_id column in the employees table and the id column in the departments table.**
```SQL
ALTER TABLE employees
ADD CONSTRAINT depID_fk
FOREIGN KEY (department_id)
REFERENCES departments(id)
```
___

**5.9) Write a SQL query to link the supplier_id column in the products table to the id column in the suppliers table using a foreign key.**
```SQL
ALTER TABLE products
ADD CONSTRAINT supplierID_FK
FOREIGN KEY (supplier_id)
REFERENCES suppliers(id)
```
___

**5.10) Write a SQL query to create a foreign key relationship between the category_id column in the items table and the id column in the categories table.**
```SQL
ALTER TABLE items
ADD CONSTRAINT categoryID_fk
FOREIGN KEY (category_id)
REFERENCES categories(id)
```
