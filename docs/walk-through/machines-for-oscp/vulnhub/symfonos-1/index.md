# <a href='https://www.vulnhub.com/entry/symfonos-1,322/' target="blank">symfonos: 1</a>

### Quick Scanning

``` bash
┌──(Hades㉿192.168.110.131)-[0.7:14.4]~
└─$ nmap -p- --min-rate 3000 192.168.110.139
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 04:51 EST
Nmap scan report for 192.168.110.139
Host is up (0.0016s latency).
Not shown: 65530 closed ports
PORT    STATE SERVICE
22/tcp  open  ssh
25/tcp  open  smtp
80/tcp  open  http
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds

Nmap done: 1 IP address (1 host up) scanned in 2.45 seconds
```