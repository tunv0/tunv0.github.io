# Recon with nmap

## Normal Scanning

### TCP

``` bash
nmap -p- -T3 $ip -o all_tcp.nmap
```

### UDP

``` bash
sudo nmap -sU -p- $ip -o all_udp.nmap
```

### Services Enum

``` bash
ports=$(cat all_tcp.nmap | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//); echo $ports
```

``` bash
nmap -sC -sV -p$ports $ip
```

## Quick Scanning

### TCP

``` bash
nmap -p- --min-rate 3000 192.168.110.136
```

## Script

### smb-vul

``` bash
nmap --script smb-vul* -p 139,445 $ip
```

### ms-sql-brute

``` bash
nmap -p 1433 --script ms-sql-brute --script-args userdb=customuser.txt,passdb=custompass.txt <host>
```