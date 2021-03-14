# Enumeration

## DNS Enumeration

=== "Commands"

	whois

	``` bash
	whois leecybersec.com
	```

	nslookup

	``` bash
	nslookup leecybersec.com
	```

	host

	``` bash
	host -t txt mail.leecybersec.com
	```

	DNSRecon

	``` bash
	dnsrecon -d leecybersec.com -t axfr

	dnsrecon -d leecybersec.com -D ~/list-subdomain.txt -t brt
	```

	DNSenum

	``` bash
	dnsenum leecybersec.com
	```

=== "Options"

	`NS` - Nameserver records contain the name of the authoritative servers hosting the DNS records for a domain.

	`A` - Also known as a host record, the "a record" contains the IP address of a hostname (such as mail.leecybersec.com).

	`MX` - Mail Exchange records contain the names of the servers responsible for handling email for the domain. A domain can contain multiple MX records.

	`PTR` - PointerRecords are used in reverse lookup zones and are used to find the records associated with an IP address.

	`CNAME` - Canonical Name Records are used to create aliases for other host records.

	`TXT` - Text records can contain any arbitrary data and can be used for various purposes, such as domain ownership verification.

=== "Script"

	``` bash
	#!/bin/bash

	if [ -z "$1" ]; then
		echo "[*] Simple Zone transfer script"
		echo "[*] Usage   : $0 <domain name> "exit 0
	fi

	for server in $(host -t ns $1 | cut -d " " -f4); do
		host -l $1 $server | grep "has address"
	done
	```

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

smb-vul

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