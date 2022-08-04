[up](../index.md)

# Database FEB06 - MEI, Normalization

## Housekeeping

- Practice Exercise 3 released today, due Monday FEB11
- Homework 3 due...? Dropbox not created

## MEI

`M.E.I` stands for *Must Exist In*

MEI is used to constrain inserts. Example used in class:

```
Advisor(departmentID) Must Exist In Major(departmentID)
```

In this case, we cannot insert an advisor with a departmentID that doesn't already exist. If we want to, we must first create their department.

## Normalization

1. First Normal Form
2. Second Normal Form
3. Third Normal Form
4. Boyce-Codd Normal Form

[Here's a good explanation of what normalization is](https://www.studytonight.com/dbms/database-normalization.php)

### For a table to be a relation

- All cells must be a single value - no arrays
    - This breaks on books with multiple authors
- Each column has a unique name
- All values in a column are of the same type
- No two rows can be identical
- Order of rows and columns is not relevant

### Essence of Normalization

- Any relation that has two or more themes should be broken up into two or more relations
- Each of these new relations has one theme.

> Let's see what the internet says

- Eliminating reduntant(useless) data.
    - This is what jim means by separating themes
    - Data must only be updated in one place
- Ensuring data dependencies make sense i.e data is logically stored.

### Anomalies

Anomalies must be avoided.

- Insert Anomaly
    - Must insert too much data
- Update Anomaly
    - Data must be changed in multiple colleges
- Delete Anomaly
    - Losing too much data
    - eg. deleting all students looses all department names

### 1NF

For a table to be in 1NF, the following conditions must be met:

- The table is a relation (see above)
-
