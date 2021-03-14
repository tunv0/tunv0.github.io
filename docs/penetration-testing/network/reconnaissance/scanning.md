# Scanning

## [Nmap Cheat Sheet](https://www.stationx.net/nmap-cheat-sheet)

## Network Sweeping

``` bash
nmap -sn 192.168.11.0/24
```

``` bash
nmap -sP 192.168.11.0/24
```

## Quick Scanning

``` bash
nmap --top-port 100 $ip
```

## Netcat Scan

TCP

``` bash
nc -nv -w 1 -z $ip 1-65535
```

UDP

``` bash
nc -nv -w 1 -z -u $ip 1-65535
```

## Masscan

TCP

``` bash
sudo masscan -i tun0 $ip -p0-65535 --rate 1000
```

``` bash
sudo masscan -p80 192.168.11.0/24
```

UDP

``` bash
masscan -pU 53 $ip
```

## All ports and Services

Grep ports

``` bash
ports=$(nmap -p- --min-rate 1000 $ip | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//)
```

TCP connect scan (-sT) takes much longer to complete than SYN scan (-sS).

SYN Scan

``` bash
sudo nmap -sS -p- --min-rate 1000 $ip
```

TCP Connect Scan

``` bash
sudo nmap -sT -p- --min-rate 1000 $ip
```

UDP Scan

``` bash
sudo nmap -sU -p- --min-rate 1000 $ip
```

## Services Enum

``` bash
nmap -sC -sV -p$ports $ip
```

``` bash
nmap -sC -sV -A -p$ports $ip
```

## OS Fingerprinting

``` bash
sudo nmap -O $ip
```

## NSE Scripts

smb-os-discovery

``` bash
nmap --script=smb-os-discovery $ip
```

smb-vul*

``` bash
nmap --script smb-vul* -p 139,445 $ip
```

ms-sql-brute

``` bash
nmap -p 1433 --script ms-sql-brute --script-args userdb=customuser.txt,passdb=custompass.txt <host>
```

dns-zone-transfer

``` bash
nmap --script=dns-zone-transfer -p 53 leecybersec.com
```