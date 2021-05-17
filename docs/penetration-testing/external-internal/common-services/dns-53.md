# DNS 53

## host

|Options|Decription|
|---|---|
|NS|Nameserver records contain the name of the authoritative servers hosting the DNS records for a domain.|
|A| Also known as a host record, the "a record" contains the IP address of a hostname (such as mail.leecybersec.com).|
|MX| Mail Exchange records contain the names of the servers responsible for handling email for the domain. A domain can contain multiple MX records.|
|PTR|PointerRecords are used in reverse lookup zones and are used to find the records associated with an IP address.|
|CNAME|Canonical Name Records are used to create aliases for other host records.|
|TXT|Text records can contain any arbitrary data and can be used for various purposes, such as domain ownership verification.|

Using options

``` bash
host -t txt mail.leecybersec.com
```

## whois

``` bash
whois leecybersec.com
```

## nslookup

``` bash
nslookup leecybersec.com
```

## DNSRecon

``` bash
dnsrecon -d leecybersec.com -t axfr

dnsrecon -d leecybersec.com -D ~/list-subdomain.txt -t brt
```

## DNSenum

``` bash
dnsenum leecybersec.com
```

## DNS Zone Transfer

``` bash
nmap --script=dns-zone-transfer -p 53 leecybersec.com
```

## Using zone transfer

``` bash
host -l leecybersec.com ns2.leecybersec.com
```

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