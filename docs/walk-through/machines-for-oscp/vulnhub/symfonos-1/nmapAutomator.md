---
hide:
  - toc        # Hide table of contents
---

# <a href='https://www.vulnhub.com/entry/symfonos-1,322/' target="blank">symfonos: 1</a>

## <a href='https://github.com/21y4d/nmapAutomator' target="blank">nmapAutomator</a>

```
┌──(Hades㉿192.168.110.131)-[0.7:15.0]~/autoscan/nmapAutomator
└─$ sudo ./nmapAutomator.sh 192.168.110.139 All
[sudo] password for kali: 

Running all scans on 192.168.110.139

Host is likely running Linux



---------------------Starting Nmap Quick Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 04:55 EST
Nmap scan report for 192.168.110.139
Host is up (0.000080s latency).
Not shown: 995 closed ports
PORT    STATE SERVICE
22/tcp  open  ssh
25/tcp  open  smtp
80/tcp  open  http
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
MAC Address: 00:0C:29:9B:BE:E9 (VMware)

Nmap done: 1 IP address (1 host up) scanned in 2.29 seconds



---------------------Starting Nmap Basic Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 04:55 EST
Nmap scan report for 192.168.110.139
Host is up (0.00032s latency).

PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.4p1 Debian 10+deb9u6 (protocol 2.0)
| ssh-hostkey: 
|   2048 ab:5b:45:a7:05:47:a5:04:45:ca:6f:18:bd:18:03:c2 (RSA)
|   256 a0:5f:40:0a:0a:1f:68:35:3e:f4:54:07:61:9f:c6:4a (ECDSA)
|_  256 bc:31:f5:40:bc:08:58:4b:fb:66:17:ff:84:12:ac:1d (ED25519)
25/tcp  open  smtp        Postfix smtpd
|_smtp-commands: symfonos.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8, 
80/tcp  open  http        Apache httpd 2.4.25 ((Debian))
|_http-server-header: Apache/2.4.25 (Debian)
|_http-title: Site doesn't have a title (text/html).
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 4.5.16-Debian (workgroup: WORKGROUP)
MAC Address: 00:0C:29:9B:BE:E9 (VMware)
Service Info: Hosts:  symfonos.localdomain, SYMFONOS; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1h59m59s, deviation: 3h27m51s, median: -1s
|_nbstat: NetBIOS name: SYMFONOS, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.5.16-Debian)
|   Computer name: symfonos
|   NetBIOS computer name: SYMFONOS\x00
|   Domain name: \x00
|   FQDN: symfonos
|_  System time: 2021-01-28T03:55:46-06:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-01-28T09:55:45
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 50.07 seconds



----------------------Starting Nmap UDP Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 04:56 EST
Warning: 192.168.110.139 giving up on port because retransmission cap hit (1).
Nmap scan report for 192.168.110.139
Host is up (0.00051s latency).
All 1000 scanned ports on 192.168.110.139 are open|filtered (978) or closed (22)
MAC Address: 00:0C:29:9B:BE:E9 (VMware)

Nmap done: 1 IP address (1 host up) scanned in 17.51 seconds



---------------------Starting Nmap Full Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 04:56 EST
Initiating ARP Ping Scan at 04:56
Scanning 192.168.110.139 [1 port]
Completed ARP Ping Scan at 04:56, 0.05s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 04:56
Completed Parallel DNS resolution of 1 host. at 04:56, 0.32s elapsed
Initiating SYN Stealth Scan at 04:56
Scanning 192.168.110.139 [65535 ports]
Discovered open port 139/tcp on 192.168.110.139
Discovered open port 25/tcp on 192.168.110.139
Discovered open port 80/tcp on 192.168.110.139
Discovered open port 22/tcp on 192.168.110.139
Discovered open port 445/tcp on 192.168.110.139
SYN Stealth Scan Timing: About 23.16% done; ETC: 04:58 (0:01:43 remaining)
SYN Stealth Scan Timing: About 46.05% done; ETC: 04:58 (0:01:11 remaining)
SYN Stealth Scan Timing: About 68.93% done; ETC: 04:58 (0:00:41 remaining)
Completed SYN Stealth Scan at 04:58, 131.07s elapsed (65535 total ports)
Nmap scan report for 192.168.110.139
Host is up (0.00030s latency).
Not shown: 65530 closed ports
PORT    STATE SERVICE
22/tcp  open  ssh
25/tcp  open  smtp
80/tcp  open  http
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
MAC Address: 00:0C:29:9B:BE:E9 (VMware)

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 131.59 seconds
           Raw packets sent: 65536 (2.884MB) | Rcvd: 65536 (2.621MB)


No new ports
                                                                                                                                                                           



---------------------Starting Nmap Vulns Scan---------------------
                                                                                                                                                                           
Running CVE scan on basic ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 04:58 EST
Nmap scan report for 192.168.110.139
Host is up (0.00030s latency).

PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.4p1 Debian 10+deb9u6 (protocol 2.0)
| vulners: 
|   cpe:/a:openbsd:openssh:7.4p1: 
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
25/tcp  open  smtp        Postfix smtpd
80/tcp  open  http        Apache httpd 2.4.25 ((Debian))
|_http-server-header: Apache/2.4.25 (Debian)
| vulners: 
|   cpe:/a:apache:http_server:2.4.25: 
|       CVE-2017-7679   7.5     https://vulners.com/cve/CVE-2017-7679
|       CVE-2017-7668   7.5     https://vulners.com/cve/CVE-2017-7668
|       CVE-2017-3169   7.5     https://vulners.com/cve/CVE-2017-3169
|       CVE-2017-3167   7.5     https://vulners.com/cve/CVE-2017-3167
|       EXPLOITPACK:44C5118F831D55FAF4259C41D8BDA0AB    7.2     https://vulners.com/exploitpack/EXPLOITPACK:44C5118F831D55FAF4259C41D8BDA0AB    *EXPLOIT*
|       CVE-2019-0211   7.2     https://vulners.com/cve/CVE-2019-0211
|       1337DAY-ID-32502        7.2     https://vulners.com/zdt/1337DAY-ID-32502        *EXPLOIT*
|       EDB-ID:47689    5.8     https://vulners.com/exploitdb/EDB-ID:47689      *EXPLOIT*
|       1337DAY-ID-33577        5.8     https://vulners.com/zdt/1337DAY-ID-33577        *EXPLOIT*
|       SSV:96537       5.0     https://vulners.com/seebug/SSV:96537    *EXPLOIT*
|       MSF:AUXILIARY/SCANNER/HTTP/APACHE_OPTIONSBLEED  5.0     https://vulners.com/metasploit/MSF:AUXILIARY/SCANNER/HTTP/APACHE_OPTIONSBLEED   *EXPLOIT*
|       EXPLOITPACK:C8C256BE0BFF5FE1C0405CB0AA9C075D    5.0     https://vulners.com/exploitpack/EXPLOITPACK:C8C256BE0BFF5FE1C0405CB0AA9C075D    *EXPLOIT*
|       1337DAY-ID-28573        5.0     https://vulners.com/zdt/1337DAY-ID-28573        *EXPLOIT*
|       EDB-ID:47688    4.3     https://vulners.com/exploitdb/EDB-ID:47688      *EXPLOIT*
|       1337DAY-ID-33575        4.3     https://vulners.com/zdt/1337DAY-ID-33575        *EXPLOIT*
|       PACKETSTORM:152441      0.0     https://vulners.com/packetstorm/PACKETSTORM:152441      *EXPLOIT*
|       EDB-ID:46676    0.0     https://vulners.com/exploitdb/EDB-ID:46676      *EXPLOIT*
|       EDB-ID:42745    0.0     https://vulners.com/exploitdb/EDB-ID:42745      *EXPLOIT*
|       1337DAY-ID-663  0.0     https://vulners.com/zdt/1337DAY-ID-663  *EXPLOIT*
|       1337DAY-ID-601  0.0     https://vulners.com/zdt/1337DAY-ID-601  *EXPLOIT*
|       1337DAY-ID-4533 0.0     https://vulners.com/zdt/1337DAY-ID-4533 *EXPLOIT*
|       1337DAY-ID-3109 0.0     https://vulners.com/zdt/1337DAY-ID-3109 *EXPLOIT*
|_      1337DAY-ID-2237 0.0     https://vulners.com/zdt/1337DAY-ID-2237 *EXPLOIT*
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
MAC Address: 00:0C:29:9B:BE:E9 (VMware)
Service Info: Hosts:  symfonos.localdomain, SYMFONOS; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 53.64 seconds


Running Vuln scan on basic ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-28 04:59 EST
Nmap scan report for 192.168.110.139
Host is up (0.00046s latency).

PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.4p1 Debian 10+deb9u6 (protocol 2.0)
25/tcp  open  smtp        Postfix smtpd
| smtp-vuln-cve2010-4344: 
|_  The SMTP server is not Exim: NOT VULNERABLE
|_sslv2-drown: 
80/tcp  open  http        Apache httpd 2.4.25 ((Debian))
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-enum: 
|_  /manual/: Potentially interesting folder
|_http-server-header: Apache/2.4.25 (Debian)
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
MAC Address: 00:0C:29:9B:BE:E9 (VMware)
Service Info: Hosts:  symfonos.localdomain, SYMFONOS; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: false
| smb-vuln-regsvc-dos: 
|   VULNERABLE:
|   Service regsvc in Microsoft Windows systems vulnerable to denial of service
|     State: VULNERABLE
|       The service regsvc in Microsoft Windows 2000 systems is vulnerable to denial of service caused by a null deference
|       pointer. This script will crash the service if it is vulnerable. This vulnerability was discovered by Ron Bowes
|       while working on smb-enum-sessions.
|_          

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 167.24 seconds



---------------------Recon Recommendations----------------------
                                                                                                                                                                           

Web Servers Recon:
                                                                                                                                                                           
gobuster dir -w /usr/share/wordlists/dirb/common.txt -l -t 30 -e -k -x .html,.php -u http://192.168.110.139:80 -o recon/gobuster_192.168.110.139_80.txt
nikto -host 192.168.110.139:80 | tee recon/nikto_192.168.110.139_80.txt


SMB Recon:
                                                                                                                                                                           
smbmap -H 192.168.110.139 | tee recon/smbmap_192.168.110.139.txt
smbclient -L "//192.168.110.139/" -U "guest"% | tee recon/smbclient_192.168.110.139.txt
enum4linux -a 192.168.110.139 | tee recon/enum4linux_192.168.110.139.txt





Which commands would you like to run?                                                                                                                                      
All (Default), enum4linux, gobuster, nikto, smbclient, smbmap, Skip <!>

Running Default in (1) s:  


---------------------Running Recon Commands----------------------
                                                                                                                                                                           

Starting gobuster scan
                                                                                                                                                                           
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://192.168.110.139:80
[+] Threads:        30
[+] Wordlist:       /usr/share/wordlists/dirb/common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Show length:    true
[+] Extensions:     php,html
[+] Expanded:       true
[+] Timeout:        10s
===============================================================
2021/01/28 05:03:04 Starting gobuster
===============================================================
http://192.168.110.139:80/.htpasswd (Status: 403) [Size: 299]
http://192.168.110.139:80/.htpasswd.html (Status: 403) [Size: 304]
http://192.168.110.139:80/.htpasswd.php (Status: 403) [Size: 303]
http://192.168.110.139:80/.hta (Status: 403) [Size: 294]
http://192.168.110.139:80/.hta.html (Status: 403) [Size: 299]
http://192.168.110.139:80/.hta.php (Status: 403) [Size: 298]
http://192.168.110.139:80/.htaccess (Status: 403) [Size: 299]
http://192.168.110.139:80/.htaccess.html (Status: 403) [Size: 304]
http://192.168.110.139:80/.htaccess.php (Status: 403) [Size: 303]
http://192.168.110.139:80/index.html (Status: 200) [Size: 328]
http://192.168.110.139:80/index.html (Status: 200) [Size: 328]
http://192.168.110.139:80/manual (Status: 301) [Size: 319]
http://192.168.110.139:80/server-status (Status: 403) [Size: 303]
===============================================================
2021/01/28 05:03:07 Finished
===============================================================

Finished gobuster scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
Starting nikto scan
                                                                                                                                                                           
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.110.139
+ Target Hostname:    192.168.110.139
+ Target Port:        80
+ Start Time:         2021-01-28 05:03:08 (GMT-5)
---------------------------------------------------------------------------
+ Server: Apache/2.4.25 (Debian)
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Apache/2.4.25 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Server may leak inodes via ETags, header found with file /, inode: 148, size: 58c6b9bb3bc5b, mtime: gzip
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS 
+ OSVDB-3092: /manual/: Web server manual found.
+ OSVDB-3268: /manual/images/: Directory indexing found.
+ OSVDB-3233: /icons/README: Apache default file found.
+ 7915 requests: 0 error(s) and 9 item(s) reported on remote host
+ End Time:           2021-01-28 05:04:08 (GMT-5) (60 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

Finished nikto scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
Starting smbmap scan
                                                                                                                                                                           
[+] Guest session       IP: 192.168.110.139:445 Name: 192.168.110.139                                   
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        print$                                                  NO ACCESS       Printer Drivers
        helios                                                  NO ACCESS       Helios personal share
        anonymous                                               READ ONLY
        IPC$                                                    NO ACCESS       IPC Service (Samba 4.5.16-Debian)

Finished smbmap scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
Starting smbclient scan
                                                                                                                                                                           

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        helios          Disk      Helios personal share
        anonymous       Disk      
        IPC$            IPC       IPC Service (Samba 4.5.16-Debian)
SMB1 disabled -- no workgroup available

Finished smbclient scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
Starting enum4linux scan
                                                                                                                                                                           
Starting enum4linux v0.8.9 ( http://labs.portcullis.co.uk/application/enum4linux/ ) on Thu Jan 28 05:04:10 2021

 ========================== 
|    Target Information    |
 ========================== 
Target ........... 192.168.110.139
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none


 ======================================================= 
|    Enumerating Workgroup/Domain on 192.168.110.139    |
 ======================================================= 
[+] Got domain/workgroup name: WORKGROUP

 =============================================== 
|    Nbtstat Information for 192.168.110.139    |
 =============================================== 
Looking up status of 192.168.110.139
        SYMFONOS        <00> -         B <ACTIVE>  Workstation Service
        SYMFONOS        <03> -         B <ACTIVE>  Messenger Service
        SYMFONOS        <20> -         B <ACTIVE>  File Server Service
        ..__MSBROWSE__. <01> - <GROUP> B <ACTIVE>  Master Browser
        WORKGROUP       <00> - <GROUP> B <ACTIVE>  Domain/Workgroup Name
        WORKGROUP       <1d> -         B <ACTIVE>  Master Browser
        WORKGROUP       <1e> - <GROUP> B <ACTIVE>  Browser Service Elections

        MAC Address = 00-00-00-00-00-00

 ======================================== 
|    Session Check on 192.168.110.139    |
 ======================================== 
[+] Server 192.168.110.139 allows sessions using username '', password ''

 ============================================== 
|    Getting domain SID for 192.168.110.139    |
 ============================================== 
Domain Name: WORKGROUP
Domain Sid: (NULL SID)
[+] Can't determine if host is part of domain or part of a workgroup

 ========================================= 
|    OS information on 192.168.110.139    |
 ========================================= 
Use of uninitialized value $os_info in concatenation (.) or string at ./enum4linux.pl line 464.
[+] Got OS info for 192.168.110.139 from smbclient: 
[+] Got OS info for 192.168.110.139 from srvinfo:
        SYMFONOS       Wk Sv PrQ Unx NT SNT Samba 4.5.16-Debian
        platform_id     :       500
        os version      :       6.1
        server type     :       0x809a03

 ================================ 
|    Users on 192.168.110.139    |
 ================================ 
index: 0x1 RID: 0x3e8 acb: 0x00000010 Account: helios   Name:   Desc: 

user:[helios] rid:[0x3e8]

 ============================================ 
|    Share Enumeration on 192.168.110.139    |
 ============================================ 

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        helios          Disk      Helios personal share
        anonymous       Disk      
        IPC$            IPC       IPC Service (Samba 4.5.16-Debian)
SMB1 disabled -- no workgroup available

[+] Attempting to map shares on 192.168.110.139
//192.168.110.139/print$        Mapping: DENIED, Listing: N/A
//192.168.110.139/helios        Mapping: DENIED, Listing: N/A
//192.168.110.139/anonymous     Mapping: OK, Listing: OK
//192.168.110.139/IPC$  [E] Can't understand response:
NT_STATUS_OBJECT_NAME_NOT_FOUND listing \*

 ======================================================= 
|    Password Policy Information for 192.168.110.139    |
 ======================================================= 


[+] Attaching to 192.168.110.139 using a NULL share

[+] Trying protocol 139/SMB...

[+] Found domain(s):

        [+] SYMFONOS
        [+] Builtin

[+] Password Info for Domain: SYMFONOS

        [+] Minimum password length: 5
        [+] Password history length: None
        [+] Maximum password age: 37 days 6 hours 21 minutes 
        [+] Password Complexity Flags: 000000

                [+] Domain Refuse Password Change: 0
                [+] Domain Password Store Cleartext: 0
                [+] Domain Password Lockout Admins: 0
                [+] Domain Password No Clear Change: 0
                [+] Domain Password No Anon Change: 0
                [+] Domain Password Complex: 0

        [+] Minimum password age: None
        [+] Reset Account Lockout Counter: 30 minutes 
        [+] Locked Account Duration: 30 minutes 
        [+] Account Lockout Threshold: None
        [+] Forced Log off Time: 37 days 6 hours 21 minutes 


[+] Retieved partial password policy with rpcclient:

Password Complexity: Disabled
Minimum Password Length: 5


 ================================= 
|    Groups on 192.168.110.139    |
 ================================= 

[+] Getting builtin groups:

[+] Getting builtin group memberships:

[+] Getting local groups:

[+] Getting local group memberships:

[+] Getting domain groups:

[+] Getting domain group memberships:

 ========================================================================== 
|    Users on 192.168.110.139 via RID cycling (RIDS: 500-550,1000-1050)    |
 ========================================================================== 
[I] Found new SID: S-1-22-1
[I] Found new SID: S-1-5-21-3173842667-3005291855-38846888
[I] Found new SID: S-1-5-32
[+] Enumerating users using SID S-1-5-32 and logon username '', password ''
S-1-5-32-500 *unknown*\*unknown* (8)
S-1-5-32-501 *unknown*\*unknown* (8)
S-1-5-32-502 *unknown*\*unknown* (8)
S-1-5-32-503 *unknown*\*unknown* (8)
S-1-5-32-504 *unknown*\*unknown* (8)
S-1-5-32-505 *unknown*\*unknown* (8)
S-1-5-32-506 *unknown*\*unknown* (8)
S-1-5-32-507 *unknown*\*unknown* (8)
S-1-5-32-508 *unknown*\*unknown* (8)
S-1-5-32-509 *unknown*\*unknown* (8)
S-1-5-32-510 *unknown*\*unknown* (8)
S-1-5-32-511 *unknown*\*unknown* (8)
S-1-5-32-512 *unknown*\*unknown* (8)
S-1-5-32-513 *unknown*\*unknown* (8)
S-1-5-32-514 *unknown*\*unknown* (8)
S-1-5-32-515 *unknown*\*unknown* (8)
S-1-5-32-516 *unknown*\*unknown* (8)
S-1-5-32-517 *unknown*\*unknown* (8)
S-1-5-32-518 *unknown*\*unknown* (8)
S-1-5-32-519 *unknown*\*unknown* (8)
S-1-5-32-520 *unknown*\*unknown* (8)
S-1-5-32-521 *unknown*\*unknown* (8)
S-1-5-32-522 *unknown*\*unknown* (8)
S-1-5-32-523 *unknown*\*unknown* (8)
S-1-5-32-524 *unknown*\*unknown* (8)
S-1-5-32-525 *unknown*\*unknown* (8)
S-1-5-32-526 *unknown*\*unknown* (8)
S-1-5-32-527 *unknown*\*unknown* (8)
S-1-5-32-528 *unknown*\*unknown* (8)
S-1-5-32-529 *unknown*\*unknown* (8)
S-1-5-32-530 *unknown*\*unknown* (8)
S-1-5-32-531 *unknown*\*unknown* (8)
S-1-5-32-532 *unknown*\*unknown* (8)
S-1-5-32-533 *unknown*\*unknown* (8)
S-1-5-32-534 *unknown*\*unknown* (8)
S-1-5-32-535 *unknown*\*unknown* (8)
S-1-5-32-536 *unknown*\*unknown* (8)
S-1-5-32-537 *unknown*\*unknown* (8)
S-1-5-32-538 *unknown*\*unknown* (8)
S-1-5-32-539 *unknown*\*unknown* (8)
S-1-5-32-540 *unknown*\*unknown* (8)
S-1-5-32-541 *unknown*\*unknown* (8)
S-1-5-32-542 *unknown*\*unknown* (8)
S-1-5-32-543 *unknown*\*unknown* (8)
S-1-5-32-544 BUILTIN\Administrators (Local Group)
S-1-5-32-545 BUILTIN\Users (Local Group)
S-1-5-32-546 BUILTIN\Guests (Local Group)
S-1-5-32-547 BUILTIN\Power Users (Local Group)
S-1-5-32-548 BUILTIN\Account Operators (Local Group)
S-1-5-32-549 BUILTIN\Server Operators (Local Group)
S-1-5-32-550 BUILTIN\Print Operators (Local Group)
S-1-5-32-1000 *unknown*\*unknown* (8)
S-1-5-32-1001 *unknown*\*unknown* (8)
S-1-5-32-1002 *unknown*\*unknown* (8)
S-1-5-32-1003 *unknown*\*unknown* (8)
S-1-5-32-1004 *unknown*\*unknown* (8)
S-1-5-32-1005 *unknown*\*unknown* (8)
S-1-5-32-1006 *unknown*\*unknown* (8)
S-1-5-32-1007 *unknown*\*unknown* (8)
S-1-5-32-1008 *unknown*\*unknown* (8)
S-1-5-32-1009 *unknown*\*unknown* (8)
S-1-5-32-1010 *unknown*\*unknown* (8)
S-1-5-32-1011 *unknown*\*unknown* (8)
S-1-5-32-1012 *unknown*\*unknown* (8)
S-1-5-32-1013 *unknown*\*unknown* (8)
S-1-5-32-1014 *unknown*\*unknown* (8)
S-1-5-32-1015 *unknown*\*unknown* (8)
S-1-5-32-1016 *unknown*\*unknown* (8)
S-1-5-32-1017 *unknown*\*unknown* (8)
S-1-5-32-1018 *unknown*\*unknown* (8)
S-1-5-32-1019 *unknown*\*unknown* (8)
S-1-5-32-1020 *unknown*\*unknown* (8)
S-1-5-32-1021 *unknown*\*unknown* (8)
S-1-5-32-1022 *unknown*\*unknown* (8)
S-1-5-32-1023 *unknown*\*unknown* (8)
S-1-5-32-1024 *unknown*\*unknown* (8)
S-1-5-32-1025 *unknown*\*unknown* (8)
S-1-5-32-1026 *unknown*\*unknown* (8)
S-1-5-32-1027 *unknown*\*unknown* (8)
S-1-5-32-1028 *unknown*\*unknown* (8)
S-1-5-32-1029 *unknown*\*unknown* (8)
S-1-5-32-1030 *unknown*\*unknown* (8)
S-1-5-32-1031 *unknown*\*unknown* (8)
S-1-5-32-1032 *unknown*\*unknown* (8)
S-1-5-32-1033 *unknown*\*unknown* (8)
S-1-5-32-1034 *unknown*\*unknown* (8)
S-1-5-32-1035 *unknown*\*unknown* (8)
S-1-5-32-1036 *unknown*\*unknown* (8)
S-1-5-32-1037 *unknown*\*unknown* (8)
S-1-5-32-1038 *unknown*\*unknown* (8)
S-1-5-32-1039 *unknown*\*unknown* (8)
S-1-5-32-1040 *unknown*\*unknown* (8)
S-1-5-32-1041 *unknown*\*unknown* (8)
S-1-5-32-1042 *unknown*\*unknown* (8)
S-1-5-32-1043 *unknown*\*unknown* (8)
S-1-5-32-1044 *unknown*\*unknown* (8)
S-1-5-32-1045 *unknown*\*unknown* (8)
S-1-5-32-1046 *unknown*\*unknown* (8)
S-1-5-32-1047 *unknown*\*unknown* (8)
S-1-5-32-1048 *unknown*\*unknown* (8)
S-1-5-32-1049 *unknown*\*unknown* (8)
S-1-5-32-1050 *unknown*\*unknown* (8)
[+] Enumerating users using SID S-1-5-21-3173842667-3005291855-38846888 and logon username '', password ''
S-1-5-21-3173842667-3005291855-38846888-500 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-501 SYMFONOS\nobody (Local User)
S-1-5-21-3173842667-3005291855-38846888-502 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-503 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-504 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-505 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-506 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-507 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-508 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-509 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-510 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-511 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-512 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-513 SYMFONOS\None (Domain Group)
S-1-5-21-3173842667-3005291855-38846888-514 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-515 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-516 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-517 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-518 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-519 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-520 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-521 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-522 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-523 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-524 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-525 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-526 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-527 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-528 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-529 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-530 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-531 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-532 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-533 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-534 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-535 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-536 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-537 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-538 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-539 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-540 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-541 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-542 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-543 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-544 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-545 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-546 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-547 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-548 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-549 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-550 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1000 SYMFONOS\helios (Local User)
S-1-5-21-3173842667-3005291855-38846888-1001 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1002 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1003 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1004 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1005 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1006 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1007 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1008 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1009 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1010 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1011 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1012 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1013 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1014 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1015 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1016 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1017 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1018 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1019 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1020 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1021 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1022 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1023 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1024 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1025 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1026 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1027 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1028 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1029 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1030 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1031 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1032 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1033 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1034 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1035 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1036 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1037 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1038 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1039 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1040 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1041 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1042 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1043 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1044 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1045 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1046 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1047 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1048 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1049 *unknown*\*unknown* (8)
S-1-5-21-3173842667-3005291855-38846888-1050 *unknown*\*unknown* (8)
[+] Enumerating users using SID S-1-22-1 and logon username '', password ''
S-1-22-1-1000 Unix User\helios (Local User)

 ================================================ 
|    Getting printer info for 192.168.110.139    |
 ================================================ 
No printers returned.


enum4linux complete on Thu Jan 28 05:04:28 2021


Finished enum4linux scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
                                                                                                                                                                           
                                                                                                                                                                           
---------------------Finished all Nmap scans---------------------                                                                                                          
                                                                                                                                                                           

Completed in 8 minute(s) and 57 second(s)
```