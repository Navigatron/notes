[up](../index.md)

# Database, JAN30

## Hosekeeping

- MyCourses has things
    - Week 3 powerpoint
    - Book excerpt "sql 63-69"
        - has good example of "normal form 1"
    - Commands and notes and such
    - Colleges_UML_01_28
        - good example of Join

## Database Stew

Database stew is not like a sad burrito.

In a sad burrito, you might get a bite of just salsa, then a few bites of rice, etc.

In Database stew, we get a taste of everything at once.

For example:

1NF = Normal Form 1

TinyInt is a single byte of storage, unsigned holds 0-255
smallint, when unsigned, holds up to ~65k

DESCRIBE will show information about a table, and EXPLAIN will do the same thing.

Midterm question: "How do you see the makeup of the table, with metadata?"

answer: `SHOW CREATE TABLE`

there is test data on the following slides of todays powerpoint:

slides 1, 2, 4, 6, 11, 12, 13, 15

slide 15 helps with HW number 3.

There rules determine if a DB is in 1NF:

- Rows contain data about the records
- Cells hold a single value
- Columns contain data about attributes
- All entries in a table are "of the same domain"
- Each column has a unique name
- Order of attributes is not important
- Order of records is not important
- No two records may be identical

All SQL terms can be broken into 3 terms

- DDL - Data Definition
    - CREATE...
- DML - Data manipulation
    - INSERT
    - SELECT
    - DELETE
    - UPDATE
- DCL - Data Control - Roll back DB to time where it is correct

HW#3 is due at some point
