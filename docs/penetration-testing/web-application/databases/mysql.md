# Mysql

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

``` bash
SELECT LOAD_FILE('/var/lib/mysql-files/pentest.txt');
```