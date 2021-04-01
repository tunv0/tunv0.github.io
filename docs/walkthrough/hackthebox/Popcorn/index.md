# HackTheBox Popcorn

> Author: Hades

> [*Scripting here*](https://github.com/leecybersec/scripting)

![](images/1.png)

## Information Gathering

### Openning Services

```
┌──(Hades㉿10.10.14.5)-[0.8:25.5]~/scripting
└─$ sudo ./enum/all.sh 10.10.10.6
[sudo] password for kali: 

### Port Scanning ############################
nmap -sS -p- --min-rate 1000 10.10.10.6 | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//

[+] Openning ports: 22,80

### Services Enumeration ############################
nmap -sC -sV -Pn 10.10.10.6 -p22,80
Starting Nmap 7.91 ( https://nmap.org ) at 2021-04-01 05:15 EDT
Nmap scan report for 10.10.10.6
Host is up (0.25s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 5.1p1 Debian 6ubuntu2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 3e:c8:1b:15:21:15:50:ec:6e:63:bc:c5:6b:80:7b:38 (DSA)
|_  2048 aa:1f:79:21:b8:42:f4:8a:38:bd:b8:05:ef:1a:07:4d (RSA)
80/tcp open  http    Apache httpd 2.2.12 ((Ubuntu))
|_http-server-header: Apache/2.2.12 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.14 seconds
```

### Apache httpd 2.2.12

List of the hidden with gobuster

```
### Web Enumeration (80) ############################

[+] Files and directories
gobuster dir -k -u http://10.10.10.6:80 -w /usr/share/seclists/Discovery/Web-Content/common.txt
<snip>
===============================================================
/.hta                 (Status: 403) [Size: 282]
/.htaccess            (Status: 403) [Size: 287]
/.htpasswd            (Status: 403) [Size: 287]
/cgi-bin/             (Status: 403) [Size: 286]
/index                (Status: 200) [Size: 177]
/index.html           (Status: 200) [Size: 177]
/test                 (Status: 200) [Size: 47041]
/torrent              (Status: 301) [Size: 310] [--> http://10.10.10.6/torrent/]
                                                                                
<snip>
```

### Torrent Hoster

Torrent Hoster hosted at `http://10.10.10.6/torrent/`

## Foothold

### 

## Privilege Escalation

###