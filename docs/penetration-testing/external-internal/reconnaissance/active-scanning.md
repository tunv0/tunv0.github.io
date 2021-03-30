# Scanning

## Network Sweeping

[*Scripting here*](https://github.com/leecybersec/scripting/tree/master/sweeping)

=== "ping"

	``` bash
	#!/bin/bash

	if [ -z $1 ]; then
		echo "Usage: $0 <SubIP>"
		exit
	fi

	for ip in $(seq 1 254); do
	   ping -c 1 $1.$ip | grep "bytes from" | cut -d " " -f 4 | cut -d ":" -f 1 &
	done
	```

=== "nmap"

	``` bash
	nmap -sn 192.168.11.0/24
	```

=== "netdiscover"

	``` bash
	netdiscover -r 192.168.11.0/24
	```

## Open Port Scanning

[*Scripting here*](https://github.com/leecybersec/scripting/tree/master/portOpenning)

=== "Netcat"

	TCP

	``` bash
	nc -nv -w 1 -z $ip 1-65535
	```

	UDP

	``` bash
	nc -nv -w 1 -z -u $ip 1-65535
	```

=== "Masscan"

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

=== "Nmap"

	Quick scan

	``` bash
	nmap --top-port 100 $ip
	```

	Grep ports

	``` bash
	ports=$(nmap -p- --min-rate 1000 $ip | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//)
	```

	TCP connect scan (-sT) takes much longer to complete than SYN scan (-sS).

	SYN Scan

	``` bash
	sudo nmap -sS -p- $ip
	```

	TCP Connect Scan

	``` bash
	sudo nmap -sT -p- $ip
	```

	UDP Scan

	``` bash
	sudo nmap -sU -p- $ip
	```

## Service Enumeration

[*Scripting here*](https://github.com/leecybersec/scripting/tree/master/enum)

[Common Services](/penetration-testing/external-internal/common-services/general/)

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

vuln

``` bash
sudo nmap --script=vuln $ip
```

smb-os-discovery

``` bash
sudo nmap --script=smb-os-discovery $ip
```

smb-vul*

``` bash
sudo nmap --script smb-vul* -p 139,445 $ip
```

ms-sql-brute

``` bash
sudo nmap -p 1433 --script ms-sql-brute --script-args userdb=customuser.txt,passdb=custompass.txt <host>
```

dns-zone-transfer

``` bash
sudo nmap --script=dns-zone-transfer -p 53 leecybersec.com
```

## [Nmap Cheat Sheet](https://www.stationx.net/nmap-cheat-sheet)

## Exploit Resources

=== "Online"

	[Exploit Database]( https://www.exploit-db.com)

	[SecurityFocus]( https://www.securityfocus.com)

	[Packet Storm](https://packetstormsecurity.com)

=== "Offline"

	SearchSploit

	``` bash
	i686-w64-mingw32-gcc 42341.c -o syncbreeze_exploit.exe -lws2_3

	wine32 syncbreeze_exploit.exe
	```

	Nmap NSE Scripts

	``` bash
	cd /usr/share/nmap/scripts
	grep Exploits *.nse
	nmap --script-help=clamav-exec.nse
	```

	Metasploit Framework

	BeEF