# 8 - Truncate tables
___

**8.1) Remove all rows from the "Employees" table but keep the table structure.**

```SQL
DELETE FROM Employees
```
___

**8.2) Write a SQL query to truncate a table and reset its identity (auto-increment) values to start from the initial seed.**
```SQL
TRUNCATE TABLE tableName
```
___

**8.3) Write a SQL query to truncate multiple tables in a single transaction while preserving foreign key relationships.**
```SQL
BEGIN TRY

    BEGIN TRANSACTION;

    -- Temporary stop checking the constraints
    ALTER Table1 NOCHECK CONSTRAINT ALL
    ALTER Table2 NOCHECK CONSTRAINT ALL

    TRUNCATE TABLE Table1
    TRUNCATE TABLE Table2

    --  Re-check the constraints again
    ALTER Table1 CHECK CONSTRAINT ALL
    ALTER Table2 CHECK CONSTRAINT ALL

    COMMIT

END TRY    
BEGIN CATCH

    ROLLBACK    

END CATCH    
```