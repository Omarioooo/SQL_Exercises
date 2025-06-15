# 4 - Drop columns
___

**4.1) Remove the "Department" column from the "Employees" table.**

```SQL
ALTER TABLE Employees
DROP COLUMN Department
```
___

**4.2) Write a SQL Server query to drop a column from a table only if it exists.**
```SQL
IF EXISTS (
    SELECT *
    FROM INFORMATION_SCHEMA.COLUMNS 
    WHERE TABLE_NAME = 'tableName' AND COLUMN_NAME = 'colName'
)
BEGIN
    ALTER TABLE tableName
    DROP COLUMN colName
END
```
___

**4.3) Write a SQL query to remove multiple columns in one ALTER TABLE statement, ensuring proper order of removal.**
```SQL
ALTER TABLE tableName
DROP COLUMN col1, col2, col3
```
___

**4.4) Write a SQL query to drop a column with a reserved keyword as its name by properly quoting the identifier.**
```SQL
ALTER TABLE tableName
DROP COLUMN [colWithReservedName] -- put the reserved keyword between [] like '[SELECT]' to avoid errors
```