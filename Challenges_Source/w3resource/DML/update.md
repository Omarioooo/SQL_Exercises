# 2 - Updating records into table
___

**2.1) Update the salary of an employee with EmployeeID = 1.**

```SQL
UPDATE Employees
SET salary = 459302
WHERE EmployeeID = 1;
```
___

**2.2) Write a SQL query to update a single record in the 'employees' table, setting a column's value based on a subquery that retrieves data from the 'salaries' table.**

```SQL
UPDATE Employees
SET salary = (
    SELECT TOP 1 salary + (salary * .1)
    FROM Salaries
    ORDER BY salary DESC
)
WHERE EmployeeID = 3;
```
___

**2.3) Write a SQL query to update a single record using a CASE expression to conditionally modify a column's value.**

```SQL
UPDATE Employees
SET salary = CASE
      WHEN salary >= 25000 THEN salary * 1.080 
      WHEN salary >= 20000 THEN salary * 1.050 
      WHEN salary >= 12000 THEN salary * 1.100 
      WHEN salary >= 10000 THEN salary * 1.125 
      WHEN salary >= 8000  THEN salary * 1.250
      ELSE salary * 1.500
    END
WHERE id = 8;
```
___

**2.4) Write a SQL query to update records where the WHERE clause involves multiple conditions combined with AND/OR operators.**

```SQL
UPDATE 
    Employees
SET 
    salary = CASE
        WHEN age >= 25 THEN salary * 1.080 
        WHEN age >= 30 THEN salary * 1.050 
        WHEN age >= 35 THEN salary * 1.100 
        WHEN age >= 40 THEN salary * 1.125 
        WHEN age >= 45 THEN salary * 1.250
        ELSE salary * 1.500
    END
WHERE
    Rate > .78
  OR
    expYears > 8  ;
```
___

**2.5) Write a SQL query to update a single record in one table by joining it with another table to determine the new value.**

```SQL
UPDATE E
SET E.salary = SE.salary + M.salary
FROM Employees E
JOIN softwareEng SE ON E.empID = SE.empID
JOIN marketing M ON E.empID = M.empID
WHERE E.empID = 9;  
```
___

**2.6) Increase the salary of all employees aged over 30 by 10%.**

```SQL
UPDATE Employees
SET salary = salary + salary * 0.30
```