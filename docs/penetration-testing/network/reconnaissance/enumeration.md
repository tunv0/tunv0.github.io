# Enumeration

## DNS Enumeration

=== "Tools"

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

=== "Options"

	`NS` - Nameserver records contain the name of the authoritative servers hosting the DNS records for a domain.

	`A` - Also known as a host record, the "a record" contains the IP address of a hostname (such as mail.leecybersec.com).

	`MX` - Mail Exchange records contain the names of the servers responsible for handling email for the domain. A domain can contain multiple MX records.

	`PTR` - PointerRecords are used in reverse lookup zones and are used to find the records associated with an IP address.

	`CNAME` - Canonical Name Records are used to create aliases for other host records.

	`TXT` - Text records can contain any arbitrary data and can be used for various purposes, such as domain ownership verification.

## Nmap

[Nmap Cheat Sheet](https://www.stationx.net/nmap-cheat-sheet)

### Quick Scanning

``` bash
nmap --top-port 100 $ip
```

### All ports and Services

TCP

``` bash
ports=$(nmap -p- --min-rate 1000 $ip | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//)
```

UDP

``` bash
ports=$(nmap -sU -p- --min-rate 1000 $ip | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//)
```

Services Enum

``` bash
nmap -sC -sV -p$ports $ip
```

### NSE Scripts

smb-vul

``` bash
nmap --script smb-vul* -p 139,445 $ip
```

ms-sql-brute

``` bash
nmap -p 1433 --script ms-sql-brute --script-args userdb=customuser.txt,passdb=custompass.txt <host>
```