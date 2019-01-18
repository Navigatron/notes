[up](../index.md)

> I know you guys don't like physical copies... That will change...

![](https://i.kym-cdn.com/entries/icons/mobile/000/023/021/e02e5ffb5f980cd8262cf7f0ae00a4a9_press-x-to-doubt-memes-memesuper-la-noire-doubt-meme_419-238.jpg)

# Database JAN18 - Composite Primary Key, Intro to queries

Text file for today is [Here.](../bonus/JAN18-cmds.txt)

SQL file for today is [Here.](../bonus/JAN18.sql)

Getting Started:
```
mysql -u root -p --verbose
SOURCE C:\path\to\JAN18.sql
TEE C:\path\to\tee\file.txt
```

### Database structure and foreign keys

Databases are made up of *tables*.

Tables consist of multiple columns, each of which is a *field*, and has a name.

Each entry in the table can be called a Tuple, Row, Record, they're all the same.

Each table has one column with the primary key attribute - the data in the primary key field
must *uniquely* identify the record.

A column can have the *foreign key* attribute, where the data it holds is the
primary key for an entry in another table.

For example, each item in the products table has a supplierID field with the
foreign key attribute. This can be used to look up the supplier of that product in
the suppliers table.

### What's Prof up to?

I'm using the TV sql file linked above.

> This is basically notes.txt from MyCourses with my own notes on top

`DESC play` - describe the play table. Multiple fields are labeled as `PRI`, or
primary key - this means the primary key is *composite*, or made of multiple fields.

`DESC tvstation` - Channel is the primary key - each station uses a unique channel. The multiple
NULL fields allow the information to be missing.

`SELECT * FROM tvstation` - get everything out of this table. See it all.

`SELECT * FROM tvstation WHERE city = "Rochester";` - Get all the records in which the
city field is set to "Rochester".

`SELECT * FROM tvstation WHERE city IS NULL;` - this should be obvious

`SELECT channel, callLetters, phone FROM tvstation;` - Get only some specific columns.

`SHOW CREATE TABLE play;` - Displays how the table was created. This helps us see
what constraints are set, such as foreign keys.

In the play table, the channel column is a foreign key that references the channel column in the tvstation table.

`SELECT name,playDate, playTime, channel FROM play order by name;` -
Selected data is now in order, alphabetically by name. Add `DESC` to the end to
reverse the order.

`SELECT * FROM play WHERE channel IN (8, 13, 31);` - IN compares the value to all items
of a set. The set is denoted by `(8, 13, 31)`.

# END

This got real interesting real fast. Let's go.
