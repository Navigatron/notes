[up](../index.md)

# Database, JAN28

- foreign keys
- lookup tables
- MUL fields
- Join Using

## foreign keys

A field in a table can reference a record in another table.

This table, our table, the table we are working with, has a field called a **FOREIGN KEY**,
which references the **PRIMARY KEY** of a record in another table.

To make a field a foreign key, add a *constraint* during table creation, or with alter_table

```
CONSTRAINT constraint_name FOREIGN KEY local_field_name REFERENCES other_table other_field;
```

For example,

```
CONSTRAINT muffin_man_fk FOREIGN KEY muffin_man REFERENCES Muffin_Men id;
```

Our table of muffins has a field containing the ID of the baker who made this muffin.

Here is the official MySQL documentation on foreign key constraints:

```mysql
[CONSTRAINT [symbol]] FOREIGN KEY
    [index_name] (col_name, ...)
    REFERENCES tbl_name (col_name,...)
    [ON DELETE reference_option]
    [ON UPDATE reference_option]

reference_option:
    RESTRICT | CASCADE | SET NULL | NO ACTION | SET DEFAULT
```

## lookup tables

A lookup table has two fields - the ID (pk) and the actual value. This lets
items in the lookup table have a *one to many* relationship with other data.

For example, one muffin man in the lookup table can now be named responsible for
any number of muffins, as said muffins reference the muffin man's primary key.

## MUL field

Indexes / keys are used to speed-up queries.

- No Key
    - This field is not indexed
- `MUL`
    - This field is indexed
    - This field can be the same as other fields
- `PRI`
    - Primary Identification of this record
    - It must be unique
    - There can only be one column with this
    - It cannot be NULL
`UNI` make a field unique
    - It must be unique
    - There can be as many columns as you want with this
    - NULL is perfectly okay.

## Join Using

TODO
