# Script Scan

## smb-vul

``` bash
nmap --script smb-vul* -p 139,445 $ip
```

## ms-sql-brute

``` bash
nmap -p 1433 --script ms-sql-brute --script-args userdb=customuser.txt,passdb=custompass.txt <host>
```