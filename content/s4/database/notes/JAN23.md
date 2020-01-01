[up](../index.md)

# Database, Jan 23rd

## Housekeeping

- HW2 due start of class Friday

## Tee file

- make sure verbose is on
- after doing the HW, edit the tee file
    - insert comments identifying HW questions
    - Delete errors
- Header comments
    - Lastname, firstname
    - ISTE 230.05 9:00AM MWF
    - Professor Jim Habbermas
    - HW X Tee File

## LIKE

use like to search for similar strings. Like requires an exact match, trailing whitespace included.
For example, `'a'='a '` (note the trailing space) is true, while `'a' LIKE 'a '` is false.

If like requires an exact match, how does it search for similar strings?

Use wildcards:

- `_` matches a single unkown character
- `%` matches any number of unknown characters

`WHERE X LIKE 'D%v%'` will match both 'David' and 'Do not vacation here'

## E-R Diagrams

- rectangles denote the object being represented, this is the "data type", or the table name. e.g, Employees
- Ovals represent attributes of the item being described. e.g, ID number
- Ovals can further represent attributes of attributes. e.g, *firstname* is a part of *name*
- Underline the words in the oval that represents the primary key

## UML Diagram

- Big Square contains all attributes
- Big Square header is name of table
- Lines connect FKs to PKs.
    - TV antenna looking thing indicates one
    - Fan looking thing indicates many
    - e.g, multiple TV shows are on the same channel

# End

> composite primary keys are spooky
