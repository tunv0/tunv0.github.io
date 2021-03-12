---
hide:
  - toc        # Hide table of contents
---

# Recon Script

## <a href='https://github.com/leecybersec/bash-script' target="blank">bash-script</a>

``` bash
┌──(Hades㉿192.168.11.130)-[1.1:15.5]~/bash_script
└─$ ./auto_enum.sh 127.0.0.1                                            
nmap -p- --min-rate 1000 127.0.0.1 | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//
[+] 22,80
nmap -sC -sV -p22,80 127.0.0.1
Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-11 02:05 EST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000082s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.4p1 Debian 4 (protocol 2.0)
| ssh-hostkey: 
|   3072 f9:e0:96:25:2b:c5:e9:24:b9:a1:e5:27:1b:42:f1:82 (RSA)
|   256 2b:ba:a6:93:2b:e1:89:d5:e9:60:2e:8f:ae:74:22:55 (ECDSA)
|_  256 8e:8d:72:cd:38:09:1a:49:6f:4e:5b:3c:69:1a:79:e5 (ED25519)
80/tcp open  http    Apache httpd 2.4.46 ((Debian))
|_http-server-header: Apache/2.4.46 (Debian)
|_http-title: Apache2 Debian Default Page: It works
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.54 seconds
===============================================================
80
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://127.0.0.1:80
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://127.0.0.1:80
[+] Threads:        10
[+] Wordlist:       /usr/share/seclists/Discovery/Web-Content/common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2021/03/11 02:05:46 Starting gobuster
===============================================================
/.htpasswd (Status: 403)
/.hta (Status: 403)
/.htaccess (Status: 403)
/index.html (Status: 200)
/javascript (Status: 301)
/server-status (Status: 200)
===============================================================
2021/03/11 02:05:46 Finished
===============================================================
===============================================================
```

## <a href='https://github.com/21y4d/nmapAutomator' target="blank">nmapAutomator</a>

``` bash
┌──(Hades㉿10.10.14.149)-[6.0:15.2]~/autoscan/nmapAutomator
└─$ sudo ./nmapAutomator.sh 10.10.10.207 All
[sudo] password for kali: 

Running all scans on 10.10.10.207

Host is likely running Linux



---------------------Starting Nmap Quick Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-24 10:03 EST
Nmap scan report for 10.10.10.207
Host is up (0.29s latency).
Not shown: 998 filtered ports
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 19.11 seconds



---------------------Starting Nmap Basic Scan---------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-24 10:03 EST
Nmap scan report for 10.10.10.207
Host is up (0.38s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 6e:da:5c:8e:8e:fb:8e:75:27:4a:b9:2a:59:cd:4b:cb (RSA)
|   256 d5:c5:b3:0d:c8:b6:69:e4:fb:13:a3:81:4a:15:16:d2 (ECDSA)
|_  256 35:6a:ee:af:dc:f8:5e:67:0d:bb:f3:ab:18:64:47:90 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
| http-title: Legitimate Rubber Ducks | Online Store
|_Requested resource was http://10.10.10.207/shop/en/
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 19.14 seconds



----------------------Starting Nmap UDP Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-24 10:03 EST
Nmap scan report for 10.10.10.207
Host is up.                                                                                                                                                                
All 1000 scanned ports on 10.10.10.207 are open|filtered                                                                                                                   
                                                                                                                                                                           
Nmap done: 1 IP address (1 host up) scanned in 202.72 seconds                                                                                                              
                                                                                                                                                                           
                                                                                                                                                                           
                                                                                                                                                                           
---------------------Starting Nmap Full Scan----------------------                                                                                                         
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.                                                                            
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-24 10:07 EST                                                                                                            
Initiating Parallel DNS resolution of 1 host. at 10:07                                                                                                                     
Completed Parallel DNS resolution of 1 host. at 10:07, 0.04s elapsed                                                                                                       
Initiating SYN Stealth Scan at 10:07                                                                                                                                       
Scanning 10.10.10.207 [65535 ports]                                                                                                                                        
Discovered open port 22/tcp on 10.10.10.207                                                                                                                                
Discovered open port 80/tcp on 10.10.10.207
Completed SYN Stealth Scan at 10:13, 359.63s elapsed (65535 total ports)
Nmap scan report for 10.10.10.207
Host is up (0.27s latency).
Not shown: 65533 filtered ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 359.78 seconds
           Raw packets sent: 131295 (5.777MB) | Rcvd: 229 (10.076KB)


No new ports
                                                                                                                                                                           



---------------------Starting Nmap Vulns Scan---------------------
                                                                                                                                                                           
Running CVE scan on basic ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-24 10:13 EST
Nmap scan report for 10.10.10.207
Host is up (0.25s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| vulners: 
|   cpe:/a:openbsd:openssh:7.6p1: 
|       EXPLOITPACK:98FE96309F9524B8C84C508837551A19    5.8     https://vulners.com/exploitpack/EXPLOITPACK:98FE96309F9524B8C84C508837551A19    *EXPLOIT*
|       EXPLOITPACK:5330EA02EBDE345BFC9D6DDDD97F9E97    5.8     https://vulners.com/exploitpack/EXPLOITPACK:5330EA02EBDE345BFC9D6DDDD97F9E97    *EXPLOIT*
|       EDB-ID:46516    5.8     https://vulners.com/exploitdb/EDB-ID:46516      *EXPLOIT*
|       SSH_ENUM        5.0     https://vulners.com/canvas/SSH_ENUM     *EXPLOIT*
|       PACKETSTORM:150621      5.0     https://vulners.com/packetstorm/PACKETSTORM:150621      *EXPLOIT*
|       MSF:AUXILIARY/SCANNER/SSH/SSH_ENUMUSERS 5.0     https://vulners.com/metasploit/MSF:AUXILIARY/SCANNER/SSH/SSH_ENUMUSERS  *EXPLOIT*
|       EXPLOITPACK:F957D7E8A0CC1E23C3C649B764E13FB0    5.0     https://vulners.com/exploitpack/EXPLOITPACK:F957D7E8A0CC1E23C3C649B764E13FB0    *EXPLOIT*
|       EXPLOITPACK:EBDBC5685E3276D648B4D14B75563283    5.0     https://vulners.com/exploitpack/EXPLOITPACK:EBDBC5685E3276D648B4D14B75563283    *EXPLOIT*
|       EDB-ID:45939    5.0     https://vulners.com/exploitdb/EDB-ID:45939      *EXPLOIT*
|       1337DAY-ID-31730        5.0     https://vulners.com/zdt/1337DAY-ID-31730        *EXPLOIT*
|       EDB-ID:45233    4.6     https://vulners.com/exploitdb/EDB-ID:45233      *EXPLOIT*
|       PACKETSTORM:151227      0.0     https://vulners.com/packetstorm/PACKETSTORM:151227      *EXPLOIT*
|       EDB-ID:46193    0.0     https://vulners.com/exploitdb/EDB-ID:46193      *EXPLOIT*
|       1337DAY-ID-32009        0.0     https://vulners.com/zdt/1337DAY-ID-32009        *EXPLOIT*
|_      1337DAY-ID-30937        0.0     https://vulners.com/zdt/1337DAY-ID-30937        *EXPLOIT*
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
| vulners: 
|   cpe:/a:apache:http_server:2.4.29: 
|       EXPLOITPACK:44C5118F831D55FAF4259C41D8BDA0AB    7.2     https://vulners.com/exploitpack/EXPLOITPACK:44C5118F831D55FAF4259C41D8BDA0AB    *EXPLOIT*
|       CVE-2019-0211   7.2     https://vulners.com/cve/CVE-2019-0211
|       1337DAY-ID-32502        7.2     https://vulners.com/zdt/1337DAY-ID-32502        *EXPLOIT*
|       EDB-ID:47689    5.8     https://vulners.com/exploitdb/EDB-ID:47689      *EXPLOIT*
|       1337DAY-ID-33577        5.8     https://vulners.com/zdt/1337DAY-ID-33577        *EXPLOIT*
|       EDB-ID:47688    4.3     https://vulners.com/exploitdb/EDB-ID:47688      *EXPLOIT*
|       1337DAY-ID-33575        4.3     https://vulners.com/zdt/1337DAY-ID-33575        *EXPLOIT*
|       PACKETSTORM:152441      0.0     https://vulners.com/packetstorm/PACKETSTORM:152441      *EXPLOIT*
|       EDB-ID:46676    0.0     https://vulners.com/exploitdb/EDB-ID:46676      *EXPLOIT*
|       1337DAY-ID-663  0.0     https://vulners.com/zdt/1337DAY-ID-663  *EXPLOIT*
|       1337DAY-ID-601  0.0     https://vulners.com/zdt/1337DAY-ID-601  *EXPLOIT*
|       1337DAY-ID-4533 0.0     https://vulners.com/zdt/1337DAY-ID-4533 *EXPLOIT*
|       1337DAY-ID-3109 0.0     https://vulners.com/zdt/1337DAY-ID-3109 *EXPLOIT*
|_      1337DAY-ID-2237 0.0     https://vulners.com/zdt/1337DAY-ID-2237 *EXPLOIT*
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.24 seconds


Running Vuln scan on basic ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-24 10:13 EST
Pre-scan script results:
| broadcast-avahi-dos: 
|   Discovered hosts:
|     224.0.0.251
|   After NULL UDP avahi packet DoS (CVE-2011-1002).
|_  Hosts are all up (not vulnerable).
Nmap scan report for 10.10.10.207
Host is up (0.26s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| vulners: 
|   cpe:/a:openbsd:openssh:7.6p1: 
|       EXPLOITPACK:98FE96309F9524B8C84C508837551A19    5.8     https://vulners.com/exploitpack/EXPLOITPACK:98FE96309F9524B8C84C508837551A19    *EXPLOIT*
|       EXPLOITPACK:5330EA02EBDE345BFC9D6DDDD97F9E97    5.8     https://vulners.com/exploitpack/EXPLOITPACK:5330EA02EBDE345BFC9D6DDDD97F9E97    *EXPLOIT*
|       EDB-ID:46516    5.8     https://vulners.com/exploitdb/EDB-ID:46516      *EXPLOIT*
|       CVE-2019-6111   5.8     https://vulners.com/cve/CVE-2019-6111
|       SSH_ENUM        5.0     https://vulners.com/canvas/SSH_ENUM     *EXPLOIT*
|       PACKETSTORM:150621      5.0     https://vulners.com/packetstorm/PACKETSTORM:150621      *EXPLOIT*
|       MSF:AUXILIARY/SCANNER/SSH/SSH_ENUMUSERS 5.0     https://vulners.com/metasploit/MSF:AUXILIARY/SCANNER/SSH/SSH_ENUMUSERS  *EXPLOIT*
|       EXPLOITPACK:F957D7E8A0CC1E23C3C649B764E13FB0    5.0     https://vulners.com/exploitpack/EXPLOITPACK:F957D7E8A0CC1E23C3C649B764E13FB0    *EXPLOIT*
|       EXPLOITPACK:EBDBC5685E3276D648B4D14B75563283    5.0     https://vulners.com/exploitpack/EXPLOITPACK:EBDBC5685E3276D648B4D14B75563283    *EXPLOIT*
|       EDB-ID:45939    5.0     https://vulners.com/exploitdb/EDB-ID:45939      *EXPLOIT*
|       CVE-2018-15919  5.0     https://vulners.com/cve/CVE-2018-15919
|       CVE-2018-15473  5.0     https://vulners.com/cve/CVE-2018-15473
|       1337DAY-ID-31730        5.0     https://vulners.com/zdt/1337DAY-ID-31730        *EXPLOIT*
|       EDB-ID:45233    4.6     https://vulners.com/exploitdb/EDB-ID:45233      *EXPLOIT*
|       CVE-2020-14145  4.3     https://vulners.com/cve/CVE-2020-14145
|       CVE-2019-6110   4.0     https://vulners.com/cve/CVE-2019-6110
|       CVE-2019-6109   4.0     https://vulners.com/cve/CVE-2019-6109
|       CVE-2018-20685  2.6     https://vulners.com/cve/CVE-2018-20685
|       PACKETSTORM:151227      0.0     https://vulners.com/packetstorm/PACKETSTORM:151227      *EXPLOIT*
|       EDB-ID:46193    0.0     https://vulners.com/exploitdb/EDB-ID:46193      *EXPLOIT*
|       1337DAY-ID-32009        0.0     https://vulners.com/zdt/1337DAY-ID-32009        *EXPLOIT*
|_      1337DAY-ID-30937        0.0     https://vulners.com/zdt/1337DAY-ID-30937        *EXPLOIT*
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
| http-csrf: 
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=10.10.10.207
|   Found the following possible CSRF vulnerabilities: 
|     
|     Path: http://10.10.10.207:80/shop/en/
|     Form id: 
|     Form action: http://10.10.10.207/shop/en/search
|     
|     Path: http://10.10.10.207:80/shop/en/rubber-ducks-c-1/red-duck-p-3
|     Form id: 
|_    Form action: http://10.10.10.207/shop/en/search
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-enum: 
|_  /backup/: Backup folder w/ directory listing
| http-fileupload-exploiter: 
|   
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-vuln-cve2017-1001000: ERROR: Script execution failed (use -d to debug)
| vulners: 
|   cpe:/a:apache:http_server:2.4.29: 
|       EXPLOITPACK:44C5118F831D55FAF4259C41D8BDA0AB    7.2     https://vulners.com/exploitpack/EXPLOITPACK:44C5118F831D55FAF4259C41D8BDA0AB    *EXPLOIT*
|       CVE-2019-0211   7.2     https://vulners.com/cve/CVE-2019-0211
|       1337DAY-ID-32502        7.2     https://vulners.com/zdt/1337DAY-ID-32502        *EXPLOIT*
|       CVE-2018-1312   6.8     https://vulners.com/cve/CVE-2018-1312
|       CVE-2017-15715  6.8     https://vulners.com/cve/CVE-2017-15715
|       CVE-2019-10082  6.4     https://vulners.com/cve/CVE-2019-10082
|       CVE-2019-0217   6.0     https://vulners.com/cve/CVE-2019-0217
|       EDB-ID:47689    5.8     https://vulners.com/exploitdb/EDB-ID:47689      *EXPLOIT*
|       CVE-2020-1927   5.8     https://vulners.com/cve/CVE-2020-1927
|       CVE-2019-10098  5.8     https://vulners.com/cve/CVE-2019-10098
|       1337DAY-ID-33577        5.8     https://vulners.com/zdt/1337DAY-ID-33577        *EXPLOIT*
|       CVE-2020-9490   5.0     https://vulners.com/cve/CVE-2020-9490
|       CVE-2020-1934   5.0     https://vulners.com/cve/CVE-2020-1934
|       CVE-2019-10081  5.0     https://vulners.com/cve/CVE-2019-10081
|       CVE-2019-0220   5.0     https://vulners.com/cve/CVE-2019-0220
|       CVE-2019-0196   5.0     https://vulners.com/cve/CVE-2019-0196
|       CVE-2018-17199  5.0     https://vulners.com/cve/CVE-2018-17199
|       CVE-2018-17189  5.0     https://vulners.com/cve/CVE-2018-17189
|       CVE-2018-1333   5.0     https://vulners.com/cve/CVE-2018-1333
|       CVE-2018-1303   5.0     https://vulners.com/cve/CVE-2018-1303
|       CVE-2017-15710  5.0     https://vulners.com/cve/CVE-2017-15710
|       CVE-2019-0197   4.9     https://vulners.com/cve/CVE-2019-0197
|       EDB-ID:47688    4.3     https://vulners.com/exploitdb/EDB-ID:47688      *EXPLOIT*
|       CVE-2020-11993  4.3     https://vulners.com/cve/CVE-2020-11993
|       CVE-2019-10092  4.3     https://vulners.com/cve/CVE-2019-10092
|       CVE-2018-1302   4.3     https://vulners.com/cve/CVE-2018-1302
|       CVE-2018-1301   4.3     https://vulners.com/cve/CVE-2018-1301
|       CVE-2018-11763  4.3     https://vulners.com/cve/CVE-2018-11763
|       1337DAY-ID-33575        4.3     https://vulners.com/zdt/1337DAY-ID-33575        *EXPLOIT*
|       CVE-2018-1283   3.5     https://vulners.com/cve/CVE-2018-1283
|       PACKETSTORM:152441      0.0     https://vulners.com/packetstorm/PACKETSTORM:152441      *EXPLOIT*
|       EDB-ID:46676    0.0     https://vulners.com/exploitdb/EDB-ID:46676      *EXPLOIT*
|       1337DAY-ID-663  0.0     https://vulners.com/zdt/1337DAY-ID-663  *EXPLOIT*
|       1337DAY-ID-601  0.0     https://vulners.com/zdt/1337DAY-ID-601  *EXPLOIT*
|       1337DAY-ID-4533 0.0     https://vulners.com/zdt/1337DAY-ID-4533 *EXPLOIT*
|       1337DAY-ID-3109 0.0     https://vulners.com/zdt/1337DAY-ID-3109 *EXPLOIT*
|_      1337DAY-ID-2237 0.0     https://vulners.com/zdt/1337DAY-ID-2237 *EXPLOIT*
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 173.66 seconds



---------------------Recon Recommendations----------------------
                                                                                                                                                                           

Web Servers Recon:
                                                                                                                                                                           
gobuster dir -w /usr/share/wordlists/dirb/common.txt -l -t 30 -e -k -x .html,.php -u http://10.10.10.207:80 -o recon/gobuster_10.10.10.207_80.txt
nikto -host 10.10.10.207:80 | tee recon/nikto_10.10.10.207_80.txt





Which commands would you like to run?                                                                                                                                      
All (Default), gobuster, nikto, Skip <!>

Running Default in (1) s:  


---------------------Running Recon Commands----------------------
                                                                                                                                                                           

Starting gobuster scan
                                                                                                                                                                           
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.10.207:80
[+] Threads:        30
[+] Wordlist:       /usr/share/wordlists/dirb/common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Show length:    true
[+] Extensions:     html,php
[+] Expanded:       true
[+] Timeout:        10s
===============================================================
2021/01/24 10:16:53 Starting gobuster
===============================================================
http://10.10.10.207:80/.hta (Status: 403) [Size: 277]
http://10.10.10.207:80/.hta.html (Status: 403) [Size: 277]
http://10.10.10.207:80/.hta.php (Status: 403) [Size: 277]
http://10.10.10.207:80/.htpasswd (Status: 403) [Size: 277]
http://10.10.10.207:80/.htpasswd.html (Status: 403) [Size: 277]
http://10.10.10.207:80/.htpasswd.php (Status: 403) [Size: 277]
http://10.10.10.207:80/.htaccess (Status: 403) [Size: 277]
http://10.10.10.207:80/.htaccess.html (Status: 403) [Size: 277]
http://10.10.10.207:80/.htaccess.php (Status: 403) [Size: 277]
http://10.10.10.207:80/backup (Status: 301) [Size: 313]
http://10.10.10.207:80/index.php (Status: 302) [Size: 0]
http://10.10.10.207:80/index.php (Status: 302) [Size: 0]
http://10.10.10.207:80/server-status (Status: 403) [Size: 277]
http://10.10.10.207:80/shop (Status: 301) [Size: 311]
===============================================================
2021/01/24 10:22:22 Finished
===============================================================

Finished gobuster scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
Starting nikto scan
                                                                                                                                                                           
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          10.10.10.207
+ Target Hostname:    10.10.10.207
+ Target Port:        80
+ Start Time:         2021-01-24 10:22:23 (GMT-5)
---------------------------------------------------------------------------
+ Server: Apache/2.4.29 (Ubuntu)
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Root page / redirects to: /shop
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Apache/2.4.29 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Cookie LCSESSID created without the httponly flag
+ Cookie language_code created without the httponly flag
+ Cookie cart[uid] created without the httponly flag
+ Cookie currency_code created without the httponly flag
+ Retrieved x-powered-by header: LiteCart
+ OSVDB-3268: /backup/: Directory indexing found.
+ OSVDB-3092: /backup/: This might be interesting...
+ OSVDB-3092: /shop/: This might be interesting...
+ Uncommon header 'refresh' found, with contents: 0; url=http://10.10.10.207/shop/en/
+ OSVDB-3233: /icons/README: Apache default file found.
+ 7863 requests: 0 error(s) and 14 item(s) reported on remote host
+ End Time:           2021-01-24 11:10:44 (GMT-5) (2901 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

Finished nikto scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
                                                                                                                                                                           
                                                                                                                                                                           
---------------------Finished all Nmap scans---------------------                                                                                                          
                                                                                                                                                                           

Completed in 1 hour(s), 7 minute(s) and 29 second(s)
```

## <a href='https://github.com/Tib3rius/AutoRecon' target="blank">AutoRecon</a>

``` bash
┌──(Hades㉿10.10.14.149)-[0.7:15.4]~/autoscan/AutoRecon/src/autorecon
└─$ python3 autorecon.py 10.10.10.207
[*] Scanning target 10.10.10.207
/home/kali/autoscan/AutoRecon/src/autorecon/autorecon.py:503: DeprecationWarning: The explicit passing of coroutine objects to asyncio.wait() is deprecated since Python 3.8, and scheduled for removal in Python 3.11.
  done, pending = await asyncio.wait(pending, return_when=FIRST_COMPLETED)
[*] Running service detection nmap-top-20-udp on 10.10.10.207
[*] Running service detection nmap-quick on 10.10.10.207
[*] Running service detection nmap-full-tcp on 10.10.10.207
[!] Service detection nmap-top-20-udp on 10.10.10.207 returned non-zero exit code: 1
[*] Service detection nmap-quick on 10.10.10.207 finished successfully in 40 seconds
[*] Found ssh on tcp/22 on target 10.10.10.207
[*] Found http on tcp/80 on target 10.10.10.207
[*] Running task tcp/22/sslscan on 10.10.10.207
[*] Running task tcp/22/nmap-ssh on 10.10.10.207
[*] Running task tcp/80/sslscan on 10.10.10.207
[*] Running task tcp/80/nmap-http on 10.10.10.207
[*] Running task tcp/80/curl-index on 10.10.10.207
[*] Running task tcp/80/curl-robots on 10.10.10.207
[*] Running task tcp/80/wkhtmltoimage on 10.10.10.207
[*] Running task tcp/80/whatweb on 10.10.10.207
[*] Running task tcp/80/nikto on 10.10.10.207
/home/kali/autoscan/AutoRecon/src/autorecon/autorecon.py:281: DeprecationWarning: The explicit passing of coroutine objects to asyncio.wait() is deprecated since Python 3.8, and scheduled for removal in Python 3.11.
  await asyncio.wait([
[*] Task tcp/22/sslscan on 10.10.10.207 finished successfully in less than a second
[*] Task tcp/80/sslscan on 10.10.10.207 finished successfully in less than a second
[*] Running task tcp/80/gobuster on 10.10.10.207
[*] Task tcp/80/curl-robots on 10.10.10.207 finished successfully in 1 second
[*] Task tcp/80/curl-index on 10.10.10.207 finished successfully in 1 second
[*] Task tcp/80/wkhtmltoimage on 10.10.10.207 finished successfully in 5 seconds
[*] Task tcp/22/nmap-ssh on 10.10.10.207 finished successfully in 11 seconds
[*] [12:44:03] - There are 5 tasks still running on 10.10.10.207
[*] Task tcp/80/whatweb on 10.10.10.207 finished successfully in 29 seconds
[*] [12:45:03] - There are 4 tasks still running on 10.10.10.207
[*] [12:46:03] - There are 4 tasks still running on 10.10.10.207
[*] Task tcp/80/nmap-http on 10.10.10.207 finished successfully in 2 minutes, 39 seconds
[*] [12:47:03] - There are 3 tasks still running on 10.10.10.207
[*] [12:48:03] - There are 3 tasks still running on 10.10.10.207
[*] Task tcp/80/gobuster on 10.10.10.207 finished successfully in 38 minutes, 59 seconds
[*] [13:23:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:24:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:25:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:26:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:27:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:28:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:29:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:30:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:31:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:32:05] - There are 2 tasks still running on 10.10.10.207
[*] Task tcp/80/nikto on 10.10.10.207 finished successfully in 48 minutes, 39 seconds
[*] [13:33:05] - There is 1 task still running on 10.10.10.207
[*] [13:34:05] - There is 1 task still running on 10.10.10.207
[*] [13:35:05] - There is 1 task still running on 10.10.10.207
[*] [13:36:05] - There is 1 task still running on 10.10.10.207
[*] [13:37:05] - There is 1 task still running on 10.10.10.207
[*] [13:38:05] - There is 1 task still running on 10.10.10.207
[*] [13:39:05] - There is 1 task still running on 10.10.10.207
[*] [13:40:05] - There is 1 task still running on 10.10.10.207
[*] [13:41:05] - There is 1 task still running on 10.10.10.207
[*] [13:42:05] - There is 1 task still running on 10.10.10.207
[*] Service detection nmap-full-tcp on 10.10.10.207 finished successfully in 59 minutes, 42 seconds
[*] Finished scanning target 10.10.10.207 in 59 minutes, 42 seconds
[*] Finished scanning all targets in 59 minutes, 42 seconds!
```