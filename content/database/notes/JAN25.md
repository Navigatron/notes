[up](../index.md)

# Database, JAN25

## Housekeeping

HW2 due this sunday at 6PM, submission via MyCourses

## More Commands

Note: The source file provided for today has capitalization errors

```
SELECT concat(advisor.lastName, ", ", advisor.firstName) as Advisor,
    Departments.departmentName FROM Advisor JOIN Departments USING
    (departmentID) ORDER BY Advisor;
```

- The above does the following
    - Mash table Advisor and table Departments together
    - Use departmentID to line up the records in each table
    - From the mega table, return the department name column
    - From the mega table, return a column called "advisor",
        which is made of both lastname and firstname.
- CONCAT AS
    - Put multiple columsn together, and return the new column with a specific name.
    - `SELECT concat(lastName, ", ", firstName) as FullName`
- JOIN
    - Put multiple tables together so we can query both at once
    - `SELECT * FROM (tableA JOIN tableB)`
- USING
    - This is more difficult to define, apparently there is an equivalent called ON as well.
- Lookup Table
    - A table with just an ID and another column, used to prevent duplicate data
- Transitive Dependency
    - Columns that depend on each other rather than the primary key
- Looking at a table
    - Describe table
    - explain table
    - show create table
