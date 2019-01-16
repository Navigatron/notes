[up](../index.md)

# Database, JAN16

There's a new Syllabus with more office hours, perhaps more changes. Updated
version is on MyCourses.

- To Open mysql on a classroom machine
    - Windows Search: mysql start
    - Windows Search: verbose
    - password: student

> It is helpful to see what you did to get your answer

Verbose mode is good to have enabled

Verbose is activated by passing the `--verbose` command line flag

For fun and profit, edit your mysql startup shortcut to pass the flag for you.

Put `ISTE230` (course code) in subject line of emails to get past Prof's spam filters.

The word Urgent will also accomplish this.

### What is a database

A collection of multiple tables, with zero or more interactions between them.

A spreadsheet is a good representation of a relational database.

Rows, from left to right, are called "Records" or "tuples".

Databases are very efficient, stupid fast ways to store and retrieve data.

### Running Linux?

[Arch Linux guide to installing mariaDB](https://wiki.archlinux.org/index.php?title=MariaDB&redirect=no#Installation)

1. `sudo pacman -S mariadb`
2. `sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql`
3. `sudo systemctl start mariadb`
4. `sudo mysql_secure_installation`
    - This guides you through setting the root password
    - Read carefully, say yes to everything.
5. `mysql -u root -p --verbose`
6. Have Fun!

### Homework

Handout given in class

Printing available in open lab on GOL 2nd floor.

# End

woohoo dabatase
