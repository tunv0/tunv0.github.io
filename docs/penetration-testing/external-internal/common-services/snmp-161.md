# snmp 161

## Scanning

``` bash
sudo nmap -sU --open -p 161 $ip
```

``` bash
snmp-check $ip
```

## Entire MIB Tree

### Script

[https://github.com/dheiland-r7/snmp](https://github.com/dheiland-r7/snmp)

``` bash
$ ./snmpbw.pl 10.10.10.241 public 2 1
SNMP query:       10.10.10.241
Queue count:      0
SNMP SUCCESS:     10.10.10.241
```

### Manual

File `list_community`:

``` txt
public
private
manager
```

``` bash
onesixtyone -c list_community -i list_ip
```

``` bash
snmpwalk -c public -v1 -t 10 $ip
```

| Options | Numbers
|---|---|
| User Accounts | snmpwalk -c public -v1 $ip 1.3.6.1.4.1.77.1.2.25 |
| Running Programs | snmpwalk -c public -v1 $ip 1.3.6.1.2.1.25.4.2.1.2 |
| Open TCP Ports | snmpwalk -c public -v1 $ip 1.3.6.1.2.1.6.13.1.3 |
| Installed Software | snmpwalk -c public -v1 $ip 1.3.6.1.2.1.25.6.3.1.2 |
| System Processes | snmpwalk -c public -v1 $ip 1.3.6.1.2.1.25.1.6.0 |
| Processes Path | snmpwalk -c public -v1 $ip 1.3.6.1.2.1.25.4.2.1.4 |
| Storage Units | snmpwalk -c public -v1 $ip 1.3.6.1.2.1.25.2.3.1.4 |