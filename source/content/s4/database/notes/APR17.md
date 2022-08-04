[up](../index.md)

# Intro to Database and Data Modeling, April 17th

The TA is teaching today, and by god, he's amazing.

# Functions in MySQL

## Types of Functions

Some operate on Rows, some on columns.

MAX(col) returns the highest number in a column.

## Character Functions

> Strings start at index 1, not zero in mysql

UPPER() and LOWER() will convert strings to upper and lower case.

LENGTH() gets the length of a string

### Searching Strings

- INSTR(s1, s2) looks in string 1 for string 2
- LOCATE(s2, s1) looks for string 2 in string 1
- Both search for strings, just the order of args is switched.

### substring

- SUBSTR(s,b,n)
	- s = string
	- b = starting position
	- n = how many chars to print

SUBSTR("yeet",1,3) = "yee"

### Concat

CONCAT(s1,s2) combines s1 and s2 and returns the result.

CONCAT('a','b'); => 'ab'

Nested concat functions are possible, but mysql allows CONCAT to take any number of args.

`||` is the concat operator, use like `'a' || 'b' || 'c' ` => `'abc'`

**All of the following are equivalent**

```
SELECT CONCAT(CONCAT(Songs.SongTitle, ' by '), Artists.Artist) as WholeThing FROM ...
```

```
SELECT CONCAT(Songs.SongTitle, ' by ', Artists.Artist) as WholeThing FROM ...
```

```
SELECT Songs.SongTitle || ' by ' || Artists.Artist as WholeThing FROM ...
```

## Numeric Functions

### Round vs Truncate

`ROUND(n,m)` rounds n to m decimal places.

`TRUNCATE(n,m)` truncates n after m decimal places.

### Other math

`MOD(n,m)` returns remainder after n is divided by m

`AVG(column)` returns the average of values in the column.

`AVG(DISTINCT column)` returns the average of the distinct values in the column.

`COUNT(\*)` returns number of rows in the column

`COUNT(column)` returns the number of non-null rows in the column

`MIN` and `MAX` do what you expect, though they do some dark magic as well.

```
SELECT MIN(LENGTH(column)) AS MinLength FROM Songs;
```

With character attributes, MIN  returns A and MAX returns Z.

`SUM` and `SUM(DISTINCT` do as you would expect.

## GROUP BY

We can group results by one or more columns in the select list

## WHERE vs HAVING

HAVING allows the use of aggregate functions (column-based) in a WHERE-like clause.

WHERE is applied to each row of the result set to see if it is included, and goes before the group by clause.

Having also allows aliases.

SELECT &rarr; FROM &rarr; WHERE &rarr; GROUP BY &rarr; HAVING &rarr; ORDER BY;

WHERE is applied to row data first, HAVING is applied to aggregate data later. Both can be used at the same time.
