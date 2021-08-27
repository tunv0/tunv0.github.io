# mysql 3306

## Connection

``` bash
mysql -h <host> -u <user> -p<pass>
```

## Query

``` bash
show databases;
show tables;
use tables;
select * from users;
```

## Readfile

[Reading and Writing Files](https://sqlwiki.netspi.com/attackQueries/readingAndWritingFiles/#mysql)

``` bash
SELECT LOAD_FILE('/etc/passwd')
```