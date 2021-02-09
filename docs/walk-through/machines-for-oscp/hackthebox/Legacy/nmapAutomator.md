---
hide:
  - toc        # Hide table of contents
---

# <a href='https://www.hackthebox.eu/home/machines/profile/2' target="blank">Legacy</a>

## <a href='https://github.com/21y4d/nmapAutomator' target="blank">nmapAutomator</a>

```
┌──(Hades㉿10.10.14.4)-[2.5:14.4]~/autoscan/nmapAutomator
└─$ sudo ./nmapAutomator.sh 10.10.10.4 All
[sudo] password for kali: 

Running all scans on 10.10.10.4

Host is likely running Windows



---------------------Starting Nmap Quick Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-06 07:21 EST
Nmap scan report for 10.10.10.4
Host is up (0.25s latency).
Not shown: 997 filtered ports, 1 closed port
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT    STATE SERVICE
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds

Nmap done: 1 IP address (1 host up) scanned in 18.12 seconds



---------------------Starting Nmap Basic Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-06 07:21 EST
Nmap scan report for 10.10.10.4
Host is up (0.25s latency).

PORT    STATE SERVICE      VERSION
139/tcp open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp open  microsoft-ds Windows XP microsoft-ds
Service Info: OSs: Windows, Windows XP; CPE: cpe:/o:microsoft:windows, cpe:/o:microsoft:windows_xp

Host script results:
|_clock-skew: mean: -3h55m55s, deviation: 1h24m50s, median: -4h55m55s
|_nbstat: NetBIOS name: LEGACY, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:b9:2e:c6 (VMware)
| smb-os-discovery: 
|   OS: Windows XP (Windows 2000 LAN Manager)
|   OS CPE: cpe:/o:microsoft:windows_xp::-
|   Computer name: legacy
|   NetBIOS computer name: LEGACY\x00
|   Workgroup: HTB\x00
|_  System time: 2021-02-06T11:25:56+02:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_smb2-time: Protocol negotiation failed (SMB2)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 60.19 seconds



----------------------Starting Nmap UDP Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-06 07:22 EST
Nmap scan report for 10.10.10.4
Host is up.
All 1000 scanned ports on 10.10.10.4 are open|filtered

Nmap done: 1 IP address (1 host up) scanned in 201.83 seconds



---------------------Starting Nmap Full Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-06 07:26 EST
Initiating Parallel DNS resolution of 1 host. at 07:26
Completed Parallel DNS resolution of 1 host. at 07:26, 0.04s elapsed
Initiating SYN Stealth Scan at 07:26
Scanning 10.10.10.4 [65535 ports]
Discovered open port 139/tcp on 10.10.10.4
Discovered open port 445/tcp on 10.10.10.4
SYN Stealth Scan Timing: About 6.05% done; ETC: 07:34 (0:08:01 remaining)
SYN Stealth Scan Timing: About 18.76% done; ETC: 07:31 (0:04:24 remaining)
SYN Stealth Scan Timing: About 34.34% done; ETC: 07:30 (0:02:54 remaining)
SYN Stealth Scan Timing: About 45.96% done; ETC: 07:30 (0:02:22 remaining)
SYN Stealth Scan Timing: About 56.50% done; ETC: 07:30 (0:01:56 remaining)
SYN Stealth Scan Timing: About 67.66% done; ETC: 07:30 (0:01:27 remaining)
SYN Stealth Scan Timing: About 80.25% done; ETC: 07:30 (0:00:52 remaining)
Completed SYN Stealth Scan at 07:30, 270.75s elapsed (65535 total ports)
Nmap scan report for 10.10.10.4
Host is up (0.25s latency).
Not shown: 65532 filtered ports
PORT     STATE  SERVICE
139/tcp  open   netbios-ssn
445/tcp  open   microsoft-ds
3389/tcp closed ms-wbt-server

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 270.89 seconds
           Raw packets sent: 131244 (5.775MB) | Rcvd: 180 (7.208KB)


No new ports
                                                                                                                                                                           



---------------------Starting Nmap Vulns Scan---------------------
                                                                                                                                                                           
Running CVE scan on basic ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-06 07:30 EST
Nmap scan report for 10.10.10.4
Host is up (0.25s latency).

PORT    STATE SERVICE      VERSION
139/tcp open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp open  microsoft-ds Microsoft Windows XP microsoft-ds
Service Info: OSs: Windows, Windows XP; CPE: cpe:/o:microsoft:windows, cpe:/o:microsoft:windows_xp

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.85 seconds


Running Vuln scan on basic ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-06 07:30 EST
Nmap scan report for 10.10.10.4
Host is up (0.25s latency).

PORT    STATE SERVICE      VERSION
139/tcp open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp open  microsoft-ds Microsoft Windows XP microsoft-ds
Service Info: OSs: Windows, Windows XP; CPE: cpe:/o:microsoft:windows, cpe:/o:microsoft:windows_xp

Host script results:
|_samba-vuln-cve-2012-1182: NT_STATUS_ACCESS_DENIED
| smb-vuln-ms08-067: 
|   VULNERABLE:
|   Microsoft Windows system vulnerable to remote code execution (MS08-067)
|     State: LIKELY VULNERABLE
|     IDs:  CVE:CVE-2008-4250
|           The Server service in Microsoft Windows 2000 SP4, XP SP2 and SP3, Server 2003 SP1 and SP2,
|           Vista Gold and SP1, Server 2008, and 7 Pre-Beta allows remote attackers to execute arbitrary
|           code via a crafted RPC request that triggers the overflow during path canonicalization.
|           
|     Disclosure date: 2008-10-23
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2008-4250
|_      https://technet.microsoft.com/en-us/library/security/ms08-067.aspx
|_smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: ERROR: Script execution failed (use -d to debug)
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|_      https://technet.microsoft.com/en-us/library/security/ms17-010.aspx

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 28.66 seconds



---------------------Recon Recommendations----------------------
                                                                                                                                                                           

SMB Recon:
                                                                                                                                                                           
smbmap -H 10.10.10.4 | tee recon/smbmap_10.10.10.4.txt
smbclient -L "//10.10.10.4/" -U "guest"% | tee recon/smbclient_10.10.10.4.txt
nmap -Pn -p445 --script vuln -oN recon/SMB_vulns_10.10.10.4.txt 10.10.10.4





Which commands would you like to run?                                                                                                                                      
All (Default), nmap, smbclient, smbmap, Skip <!>

Running Default in (1) s:  


---------------------Running Recon Commands----------------------
                                                                                                                                                                           

Starting smbmap scan
                                                                                                                                                                           
[!] 445 not open on 10.10.10.4....

Finished smbmap scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
Starting smbclient scan
                                                                                                                                                                           
do_connect: Connection to 10.10.10.4 failed (Error NT_STATUS_IO_TIMEOUT)

Finished smbclient scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
Starting nmap scan
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-06 07:31 EST
Nmap scan report for 10.10.10.4
Host is up.

PORT    STATE    SERVICE
445/tcp filtered microsoft-ds

Nmap done: 1 IP address (1 host up) scanned in 13.44 seconds

Finished nmap scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
                                                                                                                                                                           
                                                                                                                                                                           
---------------------Finished all Nmap scans---------------------                                                                                                          
                                                                                                                                                                           

Completed in 10 minute(s) and 39 second(s)
```