# <a href='https://www.vulnhub.com/entry/solidstate-1,261/' target="blank">VulnHub SolidState: 1</a>

> Author: Hades

> [*Scripting here*](https://github.com/leecybersec/bash-script)

## Enumeration

### Openning Ports

```
┌──(Hades㉿192.168.11.140)-[1.4:12.0]~/bash-script
└─$ sudo ./auto_enum.sh 192.168.11.141

Scanning openning port ...
[+] Openning ports: 22,25,80,110,119,4555
```

### Openning Services

```
┌──(Hades㉿192.168.11.140)-[5.1:12.1]~/bash-script
└─$ nmap -sC -sV 192.168.11.141 -p22,25,80,110,119,4555
Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-15 06:41 EDT
Nmap scan report for 192.168.11.141
Host is up (0.00031s latency).

PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 7.4p1 Debian 10+deb9u1 (protocol 2.0)
| ssh-hostkey: 
|   2048 77:00:84:f5:78:b9:c7:d3:54:cf:71:2e:0d:52:6d:8b (RSA)
|   256 78:b8:3a:f6:60:19:06:91:f5:53:92:1d:3f:48:ed:53 (ECDSA)
|_  256 e4:45:e9:ed:07:4d:73:69:43:5a:12:70:9d:c4:af:76 (ED25519)
25/tcp   open  smtp        JAMES smtpd 2.3.2
|_smtp-commands: solidstate Hello nmap.scanme.org (192.168.11.140 [192.168.11.140]), PIPELINING, ENHANCEDSTATUSCODES, 
80/tcp   open  http        Apache httpd 2.4.25 ((Debian))
|_http-server-header: Apache/2.4.25 (Debian)
|_http-title: Home - Solid State Security
110/tcp  open  pop3        JAMES pop3d 2.3.2
119/tcp  open  nntp        JAMES nntpd (posting ok)
4555/tcp open  james-admin JAMES Remote Admin 2.3.2
Service Info: Host: solidstate; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.47 seconds
```

## Foothold

## Privilege escalation