# 6 - Remove constraints
___

**6.1) Remove the unique constraint "UC_Name" from the "Employees" table.**
```SQL
ALTER TABLE Employees
DROP CONSTRAINT unique_emp
```
___

**6.2) Write a SQL query to delete the check constraint that ensures positive values in the price column of the products table.**

```SQL
ALTER TABLE products
DROP CONSTRAINT posV_constraint
```

___

**6.3) Write a SQL query to remove the unique constraint from the email column in the users table.**
```SQL
ALTER TABLE user
DROP CONSTRAINT unq_mail
```
___

**6.4) Write a SQL query to drop the NOT NULL constraint from the phone_number column in the customers table.**
```SQL
ALTER TABLE customers
ALTER COLUMN phone_number INT NULL
```
___

**6.5) Write a SQL query to remove the foreign key constraint from the department_id column in the employees table.**
```SQL
ALTER TABLE employees
DROP CONSTRAINT dep_FK
```
___
> NOTE :-
> ---
> ```SQL
> SELECT [name]
> FROM sys.foreign_keys
> WHERE parent_object_id = OBJECT_ID('tableName'); 
>```
> ⚠️ Tip: To Find Foreign Key Constraint Name 
>
___