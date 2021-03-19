# snmp 161

## Scanning

``` bash
sudo nmap -sU --open -p 161 $ip
```

``` bash
onesixtyone -c list_community -i list_ip
```

=== "SNMP Enumeration"

	### Entire MIB Tree

	``` bash
	snmpwalk -c public -v1 -t 10 $ip
	```

	### Windows Users

	``` bash
	snmpwalk -c public -v1 $ip 1.3.6.1.4.1.77.1.2.25
	```

	### Windows Processes

	``` bash
	snmpwalk -c public -v1 $ip 1.3.6.1.2.1.25.4.2.1.2
	```

	### Open TCP Ports

	``` bash
	snmpwalk -c public -v1 $ip 1.3.6.1.2.1.6.13.1.3
	```

	### Installed Software

	``` bash
	snmpwalk -c public -v1 $ip 1.3.6.1.2.1.25.6.3.1.2
	```

=== "SNMP MIB values"

	- 1.3.6.1.2.1.25.1.6.0 System Processes
	- 1.3.6.1.2.1.25.4.2.1.2 Running Programs
	- 1.3.6.1.2.1.25.4.2.1.4 Processes Path
	- 1.3.6.1.2.1.25.2.3.1.4 Storage Units
	- 1.3.6.1.2.1.25.6.3.1.2 Software Name
	- 1.3.6.1.4.1.77.1.2.25 User Accounts
	- 1.3.6.1.2.1.6.13.1.3 TCP Local Ports