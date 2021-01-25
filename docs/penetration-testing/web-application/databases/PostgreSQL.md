# PostgreSQL

## Connection

``` bash
$ su postgres
Password: 
$ psql
psql (9.4.15)
Type "help" for help.
```

## Query

``` bash
postgres=# \list
postgres=# \c database_name
pentesterlab=# \d
pentesterlab=# select * from users;
```

## Readfile

``` bash
$ psql -U photoblog -W photoblog
# CREATE TABLE demo(t text);
# COPY demo from '[FILENAME]';
# SELECT * FROM demo;
```