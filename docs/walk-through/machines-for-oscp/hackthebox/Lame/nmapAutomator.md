---
hide:
  - toc        # Hide table of contents
---

# <a href='https://www.hackthebox.eu/home/machines/profile/1' target="blank">Lame</a>

## <a href='https://github.com/21y4d/nmapAutomator' target="blank">nmapAutomator</a>

```
┌──(Hades㉿10.10.14.4)-[3.4:14.5]~/autoscan/nmapAutomator
└─$ sudo ./nmapAutomator.sh 10.10.10.3 All     
[sudo] password for kali: 

Running all scans on 10.10.10.3


---------------------Starting Nmap Quick Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-05 03:51 EST
Nmap scan report for 10.10.10.3
Host is up (0.32s latency).
Not shown: 996 filtered ports
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT    STATE SERVICE
21/tcp  open  ftp
22/tcp  open  ssh
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds

Nmap done: 1 IP address (1 host up) scanned in 22.27 seconds



---------------------Starting Nmap Basic Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-05 03:51 EST
Nmap scan report for 10.10.10.3
Host is up (0.33s latency).

PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 2.3.4
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 10.10.14.4
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      vsFTPd 2.3.4 - secure, fast, stable
|_End of status
22/tcp  open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| ssh-hostkey: 
|   1024 60:0f:cf:e1:c0:5f:6a:74:d6:90:24:fa:c4:d5:6c:cd (DSA)
|_  2048 56:56:24:0f:21:1d:de:a7:2b:ae:61:b1:24:3d:e8:f3 (RSA)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 2h34m26s, deviation: 3h32m09s, median: 4m25s
| smb-os-discovery: 
|   OS: Unix (Samba 3.0.20-Debian)
|   Computer name: lame
|   NetBIOS computer name: 
|   Domain name: hackthebox.gr
|   FQDN: lame.hackthebox.gr
|_  System time: 2021-02-05T03:56:17-05:00
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_smb2-time: Protocol negotiation failed (SMB2)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 55.56 seconds



----------------------Starting Nmap UDP Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-05 03:52 EST
Nmap scan report for 10.10.10.3
Host is up (0.29s latency).
All 1000 scanned ports on 10.10.10.3 are open|filtered (997) or closed (3)

Nmap done: 1 IP address (1 host up) scanned in 76.67 seconds



---------------------Starting Nmap Full Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-05 03:53 EST
Initiating Parallel DNS resolution of 1 host. at 03:53
Completed Parallel DNS resolution of 1 host. at 03:53, 0.05s elapsed
Initiating SYN Stealth Scan at 03:53
Scanning 10.10.10.3 [65535 ports]
Discovered open port 22/tcp on 10.10.10.3
Discovered open port 21/tcp on 10.10.10.3
Discovered open port 139/tcp on 10.10.10.3
Discovered open port 445/tcp on 10.10.10.3
SYN Stealth Scan Timing: About 4.86% done; ETC: 04:04 (0:10:06 remaining)
SYN Stealth Scan Timing: About 16.31% done; ETC: 04:00 (0:05:13 remaining)
SYN Stealth Scan Timing: About 26.87% done; ETC: 03:59 (0:04:08 remaining)
SYN Stealth Scan Timing: About 36.83% done; ETC: 03:59 (0:03:28 remaining)
SYN Stealth Scan Timing: About 49.23% done; ETC: 03:58 (0:02:36 remaining)
SYN Stealth Scan Timing: About 59.22% done; ETC: 03:59 (0:02:19 remaining)
SYN Stealth Scan Timing: About 73.39% done; ETC: 03:59 (0:01:24 remaining)
SYN Stealth Scan Timing: About 81.82% done; ETC: 03:59 (0:00:58 remaining)
Discovered open port 3632/tcp on 10.10.10.3
SYN Stealth Scan Timing: About 90.56% done; ETC: 03:59 (0:00:30 remaining)
Completed SYN Stealth Scan at 03:59, 340.41s elapsed (65535 total ports)
Nmap scan report for 10.10.10.3
Host is up (0.33s latency).
Not shown: 65530 filtered ports
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3632/tcp open  distccd

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 340.58 seconds
           Raw packets sent: 131282 (5.776MB) | Rcvd: 224 (9.856KB)


Making a script scan on extra ports: 3632
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-05 03:59 EST
Nmap scan report for 10.10.10.3
Host is up (0.26s latency).

PORT     STATE SERVICE VERSION
3632/tcp open  distccd distccd v1 ((GNU) 4.2.4 (Ubuntu 4.2.4-1ubuntu4))

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.57 seconds



---------------------Starting Nmap Vulns Scan---------------------
                                                                                                                                                                           
Running CVE scan on all ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-05 03:59 EST
Nmap scan report for 10.10.10.3
Host is up (0.27s latency).

PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| vulners: 
|   cpe:/a:openbsd:openssh:4.7p1: 
|       CVE-2010-4478   7.5     https://vulners.com/cve/CVE-2010-4478
|_      SSV:60656       5.0     https://vulners.com/seebug/SSV:60656    *EXPLOIT*
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
3632/tcp open  distccd     distccd v1 ((GNU) 4.2.4 (Ubuntu 4.2.4-1ubuntu4))
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.43 seconds


Running Vuln scan on all ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-05 03:59 EST
Nmap scan report for 10.10.10.3
Host is up (0.39s latency).

PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
|_sslv2-drown: 
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| vulners: 
|   cpe:/a:openbsd:openssh:4.7p1: 
|       CVE-2010-4478   7.5     https://vulners.com/cve/CVE-2010-4478
|       CVE-2008-1657   6.5     https://vulners.com/cve/CVE-2008-1657
|       SSV:60656       5.0     https://vulners.com/seebug/SSV:60656    *EXPLOIT*
|       CVE-2017-15906  5.0     https://vulners.com/cve/CVE-2017-15906
|       CVE-2010-5107   5.0     https://vulners.com/cve/CVE-2010-5107
|       CVE-2012-0814   3.5     https://vulners.com/cve/CVE-2012-0814
|       CVE-2011-5000   3.5     https://vulners.com/cve/CVE-2011-5000
|       CVE-2011-4327   2.1     https://vulners.com/cve/CVE-2011-4327
|_      CVE-2008-3259   1.2     https://vulners.com/cve/CVE-2008-3259
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
3632/tcp open  distccd     distccd v1 ((GNU) 4.2.4 (Ubuntu 4.2.4-1ubuntu4))
| distcc-cve2004-2687: 
|   VULNERABLE:
|   distcc Daemon Command Execution
|     State: VULNERABLE (Exploitable)
|     IDs:  CVE:CVE-2004-2687
|     Risk factor: High  CVSSv2: 9.3 (HIGH) (AV:N/AC:M/Au:N/C:C/I:C/A:C)
|       Allows executing of arbitrary commands on systems running distccd 3.1 and
|       earlier. The vulnerability is the consequence of weak service configuration.
|       
|     Disclosure date: 2002-02-01
|     Extra information:
|       
|     uid=1(daemon) gid=1(daemon) groups=1(daemon)
|   
|     References:
|       https://nvd.nist.gov/vuln/detail/CVE-2004-2687
|       https://distcc.github.io/security.html
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2004-2687
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: false
|_smb-vuln-regsvc-dos: ERROR: Script execution failed (use -d to debug)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 189.42 seconds



---------------------Recon Recommendations----------------------
                                                                                                                                                                           

SMB Recon:
                                                                                                                                                                           
smbmap -H 10.10.10.3 | tee recon/smbmap_10.10.10.3.txt
smbclient -L "//10.10.10.3/" -U "guest"% | tee recon/smbclient_10.10.10.3.txt





Which commands would you like to run?                                                                                                                                      
All (Default), smbclient, smbmap, Skip <!>

Running Default in (1) s:  


---------------------Running Recon Commands----------------------
                                                                                                                                                                           

Starting smbmap scan
                                                                                                                                                                           
[+] IP: 10.10.10.3:445  Name: 10.10.10.3                                        
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        print$                                                  NO ACCESS       Printer Drivers
        tmp                                                     READ, WRITE     oh noes!
        opt                                                     NO ACCESS
        IPC$                                                    NO ACCESS       IPC Service (lame server (Samba 3.0.20-Debian))
        ADMIN$                                                  NO ACCESS       IPC Service (lame server (Samba 3.0.20-Debian))

Finished smbmap scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
Starting smbclient scan
                                                                                                                                                                           
protocol negotiation failed: NT_STATUS_CONNECTION_DISCONNECTED

Finished smbclient scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
                                                                                                                                                                           
                                                                                                                                                                           
---------------------Finished all Nmap scans---------------------                                                                                                          
                                                                                                                                                                           

Completed in 12 minute(s) and 53 second(s)
```