# 11 - Dealing with schema
___

**11.1) Create a new schema named "HR".**

```SQL
CREATE SCHEMA HR;
```
___

**11.2) Write a SQL query to create a new schema with a specified owner and explicit authorization.**
```SQL
CREATE SCHEMA new_schema AUTHORIZATION [user.name]
```
___

**11.3) Write a SQL query to create a schema only if it does not already exist, using conditional logic.**
```SQL
IF NOT EXISTS (SELECT * FROM sys.schemas WHERE name = 'new_schema')
BEGIN
    EXEC('CREATE SCHEMA new_schema')
END
```
___

**11.4) Move the "Employees" table to the "HR" schema.**
```SQL
ALTER SCHEMA HR TRANSFER dbo.Employees
```
___

**11.5) Write a SQL query to move a table along with all its dependent objects, such as indexes and constraints, to a new schema.**
```SQL
ALTER SCHEMA new_schema TRANSFER old_schema.tableName
```