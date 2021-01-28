---
hide:
  - toc        # Hide table of contents
---

# <a href='https://www.vulnhub.com/entry/pentester-lab-s2-052,206/' target="blank">Pentester Lab: S2-052</a>

## <a href='https://github.com/21y4d/nmapAutomator' target="blank">nmapAutomator</a>

```
┌──(Hades㉿172.17.0.1)-[0.8:20.6]~/autoscan/nmapAutomator
└─$ sudo ./nmapAutomator.sh 192.168.110.137 All
[sudo] password for kali: 

Running all scans on 192.168.110.137

Host is likely running Linux



---------------------Starting Nmap Quick Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-27 21:39 EST
Nmap scan report for 192.168.110.137
Host is up (0.0012s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
80/tcp open  http
MAC Address: 00:0C:29:F0:63:C9 (VMware)

Nmap done: 1 IP address (1 host up) scanned in 0.32 seconds



---------------------Starting Nmap Basic Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-27 21:39 EST
Nmap scan report for 192.168.110.137
Host is up (0.00022s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
| http-cookie-flags: 
|   /: 
|     JSESSIONID: 
|_      httponly flag not set
|_http-server-header: Apache-Coyote/1.1
| http-title: Orders
|_Requested resource was /orders.xhtml
MAC Address: 00:0C:29:F0:63:C9 (VMware)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.87 seconds



----------------------Starting Nmap UDP Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-27 21:39 EST
Warning: 192.168.110.137 giving up on port because retransmission cap hit (1).
Nmap scan report for 192.168.110.137
Host is up (0.00057s latency).
All 1000 scanned ports on 192.168.110.137 are open|filtered (976) or closed (24)
MAC Address: 00:0C:29:F0:63:C9 (VMware)

Nmap done: 1 IP address (1 host up) scanned in 19.35 seconds



---------------------Starting Nmap Full Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-27 21:40 EST
Initiating ARP Ping Scan at 21:40
Scanning 192.168.110.137 [1 port]
Completed ARP Ping Scan at 21:40, 0.07s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 21:40
Completed Parallel DNS resolution of 1 host. at 21:40, 0.04s elapsed
Initiating SYN Stealth Scan at 21:40
Scanning 192.168.110.137 [65535 ports]
Discovered open port 80/tcp on 192.168.110.137
SYN Stealth Scan Timing: About 23.06% done; ETC: 21:42 (0:01:43 remaining)
SYN Stealth Scan Timing: About 45.95% done; ETC: 21:42 (0:01:12 remaining)
SYN Stealth Scan Timing: About 68.84% done; ETC: 21:42 (0:00:41 remaining)
Completed SYN Stealth Scan at 21:42, 131.07s elapsed (65535 total ports)
Nmap scan report for 192.168.110.137
Host is up (0.00026s latency).
Not shown: 65534 closed ports
PORT   STATE SERVICE
80/tcp open  http
MAC Address: 00:0C:29:F0:63:C9 (VMware)

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 131.35 seconds
           Raw packets sent: 65536 (2.884MB) | Rcvd: 65536 (2.621MB)


No new ports
                                                                                                                                                                           



---------------------Starting Nmap Vulns Scan---------------------
                                                                                                                                                                           
Running CVE scan on basic ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-27 21:42 EST
Nmap scan report for 192.168.110.137
Host is up (0.00024s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
|_http-server-header: Apache-Coyote/1.1
MAC Address: 00:0C:29:F0:63:C9 (VMware)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.45 seconds


Running Vuln scan on basic ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-27 21:42 EST
Nmap scan report for 192.168.110.137
Host is up (0.00045s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
| http-cookie-flags: 
|   /: 
|     JSESSIONID: 
|       httponly flag not set
|   /orders/: 
|     JSESSIONID: 
|_      httponly flag not set
| http-csrf: 
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=192.168.110.137
|   Found the following possible CSRF vulnerabilities: 
|     
|     Path: http://192.168.110.137:80/orders/new
|     Form id: orders;jsessionid=6183d39106ee49094e339206c8a58e50
|     Form action: /orders;jsessionid=6183D39106EE49094E339206C8A58E50
|     
|     Path: http://192.168.110.137:80/orders/3/edit
|     Form id: 3;jsessionid=9bdd34e93ef01a0e2e36f692e08ac641
|     Form action: /orders/3;jsessionid=9BDD34E93EF01A0E2E36F692E08AC641
|     
|     Path: http://192.168.110.137:80/orders/5/edit
|     Form id: 5;jsessionid=bb8cc23d5a19d07a6693456214e1a177
|     Form action: /orders/5;jsessionid=BB8CC23D5A19D07A6693456214E1A177
|     
|     Path: http://192.168.110.137:80/orders/3/deleteConfirm
|     Form id: 
|     Form action: ../3?_method=DELETE
|     
|     Path: http://192.168.110.137:80/orders/5/deleteConfirm
|     Form id: 
|     Form action: ../5?_method=DELETE
|     
|     Path: http://192.168.110.137:80/orders/4/deleteConfirm
|     Form id: 
|     Form action: ../4?_method=DELETE
|     
|     Path: http://192.168.110.137:80/orders/4/edit
|     Form id: 4;jsessionid=d564c6a803a0cbaaad987b4de62a32a2
|_    Form action: /orders/4;jsessionid=D564C6A803A0CBAAAD987B4DE62A32A2
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-enum: 
|_  /orders/: Potentially interesting folder
|_http-server-header: Apache-Coyote/1.1
| http-slowloris-check: 
|   VULNERABLE:
|   Slowloris DOS attack
|     State: LIKELY VULNERABLE
|     IDs:  CVE:CVE-2007-6750
|       Slowloris tries to keep many connections to the target web server open and hold
|       them open as long as possible.  It accomplishes this by opening connections to
|       the target web server and sending a partial request. By doing so, it starves
|       the http server's resources causing Denial Of Service.
|       
|     Disclosure date: 2009-09-17
|     References:
|       http://ha.ckers.org/slowloris/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
MAC Address: 00:0C:29:F0:63:C9 (VMware)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 328.09 seconds



---------------------Recon Recommendations----------------------
                                                                                                                                                                           

Web Servers Recon:
                                                                                                                                                                           
gobuster dir -w /usr/share/wordlists/dirb/common.txt -l -t 30 -e -k -x .html,.php -u http://192.168.110.137:80 -o recon/gobuster_192.168.110.137_80.txt
nikto -host 192.168.110.137:80 | tee recon/nikto_192.168.110.137_80.txt





Which commands would you like to run?                                                                                                                                      
All (Default), gobuster, nikto, Skip <!>

Running Default in (1) s:  


---------------------Running Recon Commands----------------------
                                                                                                                                                                           

Starting gobuster scan
                                                                                                                                                                           
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://192.168.110.137:80
[+] Threads:        30
[+] Wordlist:       /usr/share/wordlists/dirb/common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Show length:    true
[+] Extensions:     html,php
[+] Expanded:       true
[+] Timeout:        10s
===============================================================
2021/01/27 21:48:24 Starting gobuster
===============================================================
http://192.168.110.137:80/css (Status: 302) [Size: 0]
http://192.168.110.137:80/fonts (Status: 302) [Size: 0]
http://192.168.110.137:80/META-INF (Status: 302) [Size: 0]
http://192.168.110.137:80/orders (Status: 200) [Size: 1385]
http://192.168.110.137:80/WEB-INF (Status: 302) [Size: 0]
===============================================================
2021/01/27 21:48:30 Finished
===============================================================

Finished gobuster scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
Starting nikto scan
                                                                                                                                                                           
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.110.137
+ Target Hostname:    192.168.110.137
+ Target Port:        80
+ Start Time:         2021-01-27 21:48:31 (GMT-5)
---------------------------------------------------------------------------
+ Server: Apache-Coyote/1.1
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Root page / redirects to: /orders.xhtml
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Server banner has changed from 'Apache-Coyote/1.1' to 'Apache/2.2.21 (Unix) DAV/2' which may suggest a WAF, load balancer or proxy is in place
+ Cookie JSESSIONID created without the httponly flag
+ OSVDB-3092: /orders/: This might be interesting...
+ 7915 requests: 0 error(s) and 5 item(s) reported on remote host
+ End Time:           2021-01-27 21:48:53 (GMT-5) (22 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

Finished nikto scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
                                                                                                                                                                           
                                                                                                                                                                           
---------------------Finished all Nmap scans---------------------                                                                                                          
                                                                                                                                                                           

Completed in 9 minute(s) and 15 second(s)
```