[up](../index.md)

# Sysadmin FEB08

## Linux system accounts

inside /etc/passwd

- username
- x for password if password is in /etc/shadow
- user id
- group id
- comment
- home dir
- default shell

inside /etc/shadow

- username
- salted hashed password
    - if no password, * or !
- days since last password change
- min days until password can be changed
- max days before password must be changed
- number of days for warning
- something about activation
- Account expiration date

inside /etc/group

- group name
- group password "x"
- group id
- comma list of group member usernames

The joys of the user add command

- Put this in the sitebook

## DHCP

Review from netserv, pretty simple stuff.
