# 7 - Drop tables
___

**7.1) Delete the "Departments" table permanently.**

```SQL
Drop TABLE Departments
```
___

**7.2) Write a query to drop a table only if it exists. Also, ensure that any dependent constraints are handled appropriately.**
```SQL
DROP TABLE IF EXIST tableName
```
___

**7.3) Write a SQL query to drop multiple tables within a single transaction to ensure atomicity.**
```SQL
BEGIN TRY

    BEGIN TRANSACTION;

    DROP TABLE IF EXISTS Table1
    DROP TABLE IF EXISTS Table2
    DROP TABLE IF EXISTS Table3

    COMMIT

END TRY    
BEGIN CATCH

    ROLLBACK    

END CATCH    
```

___

**7.4) Write a SQL query to drop a schema-qualified table with special characters in its name using proper quoting.**
```SQL
DROP TABLE [schema].[tableName];
```
