---
hide:
  - toc        # Hide table of contents
---

# <a href='https://www.vulnhub.com/entry/dc-9,412/' target="blank">DC: 9</a>

## <a href='https://github.com/21y4d/nmapAutomator' target="blank">nmapAutomator</a>

```
┌──(Hades㉿172.17.0.1)-[0.5:14.8]~/autoscan/nmapAutomator
└─$ sudo ./nmapAutomator.sh 192.168.110.138 All
[sudo] password for kali: 

Running all scans on 192.168.110.138

Host is likely running Linux



---------------------Starting Nmap Quick Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 02:02 EST
Nmap scan report for 192.168.110.138
Host is up (0.000076s latency).
Not shown: 998 closed ports, 1 filtered port
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE
80/tcp open  http
MAC Address: 00:0C:29:3A:3B:8C (VMware)

Nmap done: 1 IP address (1 host up) scanned in 0.31 seconds



---------------------Starting Nmap Basic Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 02:02 EST
Nmap scan report for 192.168.110.138
Host is up (0.00025s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.38 ((Debian))
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: Example.com - Staff Details - Welcome
MAC Address: 00:0C:29:3A:3B:8C (VMware)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.80 seconds



----------------------Starting Nmap UDP Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 02:02 EST
Warning: 192.168.110.138 giving up on port because retransmission cap hit (1).
Nmap scan report for 192.168.110.138
Host is up (0.00074s latency).
All 1000 scanned ports on 192.168.110.138 are open|filtered (976) or closed (24)
MAC Address: 00:0C:29:3A:3B:8C (VMware)

Nmap done: 1 IP address (1 host up) scanned in 19.30 seconds



---------------------Starting Nmap Full Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 02:03 EST
Initiating ARP Ping Scan at 02:03
Scanning 192.168.110.138 [1 port]
Completed ARP Ping Scan at 02:03, 0.07s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 02:03
Completed Parallel DNS resolution of 1 host. at 02:03, 0.05s elapsed
Initiating SYN Stealth Scan at 02:03
Scanning 192.168.110.138 [65535 ports]
Discovered open port 80/tcp on 192.168.110.138
SYN Stealth Scan Timing: About 23.20% done; ETC: 02:05 (0:01:43 remaining)
SYN Stealth Scan Timing: About 46.09% done; ETC: 02:05 (0:01:11 remaining)
SYN Stealth Scan Timing: About 68.98% done; ETC: 02:05 (0:00:41 remaining)
Completed SYN Stealth Scan at 02:05, 131.07s elapsed (65535 total ports)
Nmap scan report for 192.168.110.138
Host is up (0.00048s latency).
Not shown: 65533 closed ports
PORT   STATE    SERVICE
22/tcp filtered ssh
80/tcp open     http
MAC Address: 00:0C:29:3A:3B:8C (VMware)

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 131.37 seconds
           Raw packets sent: 65536 (2.884MB) | Rcvd: 65536 (2.621MB)


No new ports
                                                                                                                                                                           



---------------------Starting Nmap Vulns Scan---------------------
                                                                                                                                                                           
Running CVE scan on basic ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 02:05 EST
Nmap scan report for 192.168.110.138
Host is up (0.00033s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.38 ((Debian))
|_http-server-header: Apache/2.4.38 (Debian)
| vulners: 
|   cpe:/a:apache:http_server:2.4.38: 
|       CVE-2020-11984  7.5     https://vulners.com/cve/CVE-2020-11984
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
MAC Address: 00:0C:29:3A:3B:8C (VMware)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.21 seconds


Running Vuln scan on basic ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 02:05 EST
Nmap scan report for 192.168.110.138
Host is up (0.00030s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.38 ((Debian))
| http-csrf: 
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=192.168.110.138
|   Found the following possible CSRF vulnerabilities: 
|     
|     Path: http://192.168.110.138:80/manage.php
|     Form id: 
|     Form action: manage.php
|     
|     Path: http://192.168.110.138:80/search.php
|     Form id: 
|_    Form action: results.php
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-enum: 
|   /css/: Potentially interesting directory w/ listing on 'apache/2.4.38 (debian)'
|_  /includes/: Potentially interesting directory w/ listing on 'apache/2.4.38 (debian)'
|_http-server-header: Apache/2.4.38 (Debian)
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-vuln-cve2017-1001000: ERROR: Script execution failed (use -d to debug)
| vulners: 
|   cpe:/a:apache:http_server:2.4.38: 
|       CVE-2020-11984  7.5     https://vulners.com/cve/CVE-2020-11984
|       EXPLOITPACK:44C5118F831D55FAF4259C41D8BDA0AB    7.2     https://vulners.com/exploitpack/EXPLOITPACK:44C5118F831D55FAF4259C41D8BDA0AB    *EXPLOIT*
|       CVE-2019-0211   7.2     https://vulners.com/cve/CVE-2019-0211
|       1337DAY-ID-32502        7.2     https://vulners.com/zdt/1337DAY-ID-32502        *EXPLOIT*
|       CVE-2019-10082  6.4     https://vulners.com/cve/CVE-2019-10082
|       CVE-2019-10097  6.0     https://vulners.com/cve/CVE-2019-10097
|       CVE-2019-0217   6.0     https://vulners.com/cve/CVE-2019-0217
|       CVE-2019-0215   6.0     https://vulners.com/cve/CVE-2019-0215
|       EDB-ID:47689    5.8     https://vulners.com/exploitdb/EDB-ID:47689      *EXPLOIT*
|       CVE-2020-1927   5.8     https://vulners.com/cve/CVE-2020-1927
|       CVE-2019-10098  5.8     https://vulners.com/cve/CVE-2019-10098
|       1337DAY-ID-33577        5.8     https://vulners.com/zdt/1337DAY-ID-33577        *EXPLOIT*
|       CVE-2020-9490   5.0     https://vulners.com/cve/CVE-2020-9490
|       CVE-2020-1934   5.0     https://vulners.com/cve/CVE-2020-1934
|       CVE-2019-10081  5.0     https://vulners.com/cve/CVE-2019-10081
|       CVE-2019-0220   5.0     https://vulners.com/cve/CVE-2019-0220
|       CVE-2019-0196   5.0     https://vulners.com/cve/CVE-2019-0196
|       CVE-2019-0197   4.9     https://vulners.com/cve/CVE-2019-0197
|       EDB-ID:47688    4.3     https://vulners.com/exploitdb/EDB-ID:47688      *EXPLOIT*
|       CVE-2020-11993  4.3     https://vulners.com/cve/CVE-2020-11993
|       CVE-2019-10092  4.3     https://vulners.com/cve/CVE-2019-10092
|       1337DAY-ID-33575        4.3     https://vulners.com/zdt/1337DAY-ID-33575        *EXPLOIT*
|       PACKETSTORM:152441      0.0     https://vulners.com/packetstorm/PACKETSTORM:152441      *EXPLOIT*
|       EDB-ID:46676    0.0     https://vulners.com/exploitdb/EDB-ID:46676      *EXPLOIT*
|       1337DAY-ID-663  0.0     https://vulners.com/zdt/1337DAY-ID-663  *EXPLOIT*
|       1337DAY-ID-601  0.0     https://vulners.com/zdt/1337DAY-ID-601  *EXPLOIT*
|       1337DAY-ID-4533 0.0     https://vulners.com/zdt/1337DAY-ID-4533 *EXPLOIT*
|       1337DAY-ID-3109 0.0     https://vulners.com/zdt/1337DAY-ID-3109 *EXPLOIT*
|_      1337DAY-ID-2237 0.0     https://vulners.com/zdt/1337DAY-ID-2237 *EXPLOIT*
MAC Address: 00:0C:29:3A:3B:8C (VMware)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 38.60 seconds



---------------------Recon Recommendations----------------------
                                                                                                                                                                           

Web Servers Recon:
                                                                                                                                                                           
gobuster dir -w /usr/share/wordlists/dirb/common.txt -l -t 30 -e -k -x .html,.php -u http://192.168.110.138:80 -o recon/gobuster_192.168.110.138_80.txt
nikto -host 192.168.110.138:80 | tee recon/nikto_192.168.110.138_80.txt





Which commands would you like to run?                                                                                                                                      
All (Default), gobuster, nikto, Skip <!>

Running Default in (1) s:  


---------------------Running Recon Commands----------------------
                                                                                                                                                                           

Starting gobuster scan
                                                                                                                                                                           
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://192.168.110.138:80
[+] Threads:        30
[+] Wordlist:       /usr/share/wordlists/dirb/common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Show length:    true
[+] Extensions:     html,php
[+] Expanded:       true
[+] Timeout:        10s
===============================================================
2021/01/28 02:06:34 Starting gobuster
===============================================================
http://192.168.110.138:80/.htaccess (Status: 403) [Size: 280]
http://192.168.110.138:80/.htaccess.html (Status: 403) [Size: 280]
http://192.168.110.138:80/.htaccess.php (Status: 403) [Size: 280]
http://192.168.110.138:80/.hta (Status: 403) [Size: 280]
http://192.168.110.138:80/.hta.html (Status: 403) [Size: 280]
http://192.168.110.138:80/.hta.php (Status: 403) [Size: 280]
http://192.168.110.138:80/.htpasswd (Status: 403) [Size: 280]
http://192.168.110.138:80/.htpasswd.html (Status: 403) [Size: 280]
http://192.168.110.138:80/.htpasswd.php (Status: 403) [Size: 280]
http://192.168.110.138:80/config.php (Status: 200) [Size: 0]
http://192.168.110.138:80/css (Status: 301) [Size: 316]
http://192.168.110.138:80/display.php (Status: 200) [Size: 2961]
http://192.168.110.138:80/includes (Status: 301) [Size: 321]
http://192.168.110.138:80/index.php (Status: 200) [Size: 917]
http://192.168.110.138:80/index.php (Status: 200) [Size: 917]
http://192.168.110.138:80/manage.php (Status: 200) [Size: 1210]
http://192.168.110.138:80/logout.php (Status: 302) [Size: 0]
http://192.168.110.138:80/results.php (Status: 200) [Size: 1056]
http://192.168.110.138:80/server-status (Status: 403) [Size: 280]
http://192.168.110.138:80/session.php (Status: 302) [Size: 0]
http://192.168.110.138:80/search.php (Status: 200) [Size: 1091]
http://192.168.110.138:80/welcome.php (Status: 302) [Size: 0]
===============================================================
2021/01/28 02:06:44 Finished
===============================================================

Finished gobuster scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
Starting nikto scan
                                                                                                                                                                           
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.110.138
+ Target Hostname:    192.168.110.138
+ Target Port:        80
+ Start Time:         2021-01-28 02:06:45 (GMT-5)
---------------------------------------------------------------------------
+ Server: Apache/2.4.38 (Debian)
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Web Server returns a valid response with junk HTTP methods, this may cause false positives.
+ /config.php: PHP Config file may contain database IDs and passwords.
+ OSVDB-3268: /css/: Directory indexing found.
+ OSVDB-3092: /css/: This might be interesting...
+ OSVDB-3268: /includes/: Directory indexing found.
+ OSVDB-3092: /includes/: This might be interesting...
+ OSVDB-3233: /icons/README: Apache default file found.
+ 7915 requests: 0 error(s) and 10 item(s) reported on remote host
+ End Time:           2021-01-28 02:07:43 (GMT-5) (58 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested


      *********************************************************************
      Portions of the server's headers (Apache/2.4.38) are not in
      the Nikto 2.1.6 database or are newer than the known string. Would you like
      to submit this information (*no server specific data*) to CIRT.net
      for a Nikto update (or you may email to sullo@cirt.net) (y/n)? 

Finished nikto scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
                                                                                                                                                                           
                                                                                                                                                                           
---------------------Finished all Nmap scans---------------------                                                                                                          
                                                                                                                                                                           

Completed in 5 minute(s) and 5 second(s)
```