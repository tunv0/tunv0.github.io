---
hide:
  - toc        # Hide table of contents
---

# <a href='https://www.vulnhub.com/entry/pentester-lab-cve-2007-1860-mod_jk-double-decoding,82/' target="blank">Pentester Lab: CVE-2007-1860: mod_jk double-decoding</a>

## <a href='https://github.com/21y4d/nmapAutomator' target="blank">nmapAutomator</a>

```
┌──(Hades㉿192.168.110.131)-[2.9:14.1]~/autoscan/nmapAutomator
└─$ sudo ./nmapAutomator.sh 192.168.110.140 All
[sudo] password for kali: 

Running all scans on 192.168.110.140

Host is likely running Linux



---------------------Starting Nmap Quick Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-30 05:25 EST
Nmap scan report for 192.168.110.140
Host is up (0.0060s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
MAC Address: 00:0C:29:AD:E5:A2 (VMware)

Nmap done: 1 IP address (1 host up) scanned in 0.43 seconds



---------------------Starting Nmap Basic Scan---------------------

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-30 05:25 EST
Nmap scan report for 192.168.110.140
Host is up (0.00072s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 5.5p1 Debian 6+squeeze3 (protocol 2.0)
| ssh-hostkey: 
|   1024 ed:4d:4a:16:38:df:ee:90:03:95:9c:c5:52:e5:ef:f5 (DSA)
|_  2048 88:34:9a:e6:ca:58:49:44:de:1e:cf:36:42:cf:f6:2c (RSA)
80/tcp open  http    Apache httpd 2.2.16 ((Debian))
|_http-server-header: Apache/2.2.16 (Debian)
|_http-title: Apache Tomcat Examples
MAC Address: 00:0C:29:AD:E5:A2 (VMware)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.30 seconds



----------------------Starting Nmap UDP Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-30 05:25 EST
Warning: 192.168.110.140 giving up on port because retransmission cap hit (1).
Nmap scan report for 192.168.110.140
Host is up (0.00061s latency).
All 1000 scanned ports on 192.168.110.140 are open|filtered (977) or closed (23)
MAC Address: 00:0C:29:AD:E5:A2 (VMware)

Nmap done: 1 IP address (1 host up) scanned in 17.54 seconds



---------------------Starting Nmap Full Scan----------------------
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-30 05:25 EST
Initiating ARP Ping Scan at 05:25
Scanning 192.168.110.140 [1 port]
Completed ARP Ping Scan at 05:25, 0.06s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 05:25
Completed Parallel DNS resolution of 1 host. at 05:25, 0.04s elapsed
Initiating SYN Stealth Scan at 05:25
Scanning 192.168.110.140 [65535 ports]
Discovered open port 80/tcp on 192.168.110.140
Discovered open port 22/tcp on 192.168.110.140
SYN Stealth Scan Timing: About 23.24% done; ETC: 05:28 (0:01:42 remaining)
SYN Stealth Scan Timing: About 46.13% done; ETC: 05:28 (0:01:11 remaining)
SYN Stealth Scan Timing: About 69.02% done; ETC: 05:28 (0:00:41 remaining)
Completed SYN Stealth Scan at 05:28, 131.07s elapsed (65535 total ports)
Nmap scan report for 192.168.110.140
Host is up (0.00032s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
MAC Address: 00:0C:29:AD:E5:A2 (VMware)

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 131.34 seconds
           Raw packets sent: 65536 (2.884MB) | Rcvd: 65570 (2.628MB)


No new ports
                                                                                                                                                                           



---------------------Starting Nmap Vulns Scan---------------------
                                                                                                                                                                           
Running CVE scan on basic ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-30 05:28 EST
Nmap scan report for 192.168.110.140
Host is up (0.00094s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 5.5p1 Debian 6+squeeze3 (protocol 2.0)
| vulners: 
|   cpe:/a:openbsd:openssh:5.5p1: 
|       EDB-ID:40888    7.8     https://vulners.com/exploitdb/EDB-ID:40888      *EXPLOIT*
|       CVE-2010-4478   7.5     https://vulners.com/cve/CVE-2010-4478
|       EDB-ID:41173    7.2     https://vulners.com/exploitdb/EDB-ID:41173      *EXPLOIT*
|       SSV:60656       5.0     https://vulners.com/seebug/SSV:60656    *EXPLOIT*
|       SSV:90447       4.6     https://vulners.com/seebug/SSV:90447    *EXPLOIT*
|       EDB-ID:45233    4.6     https://vulners.com/exploitdb/EDB-ID:45233      *EXPLOIT*
|       EDB-ID:45210    4.6     https://vulners.com/exploitdb/EDB-ID:45210      *EXPLOIT*
|       EDB-ID:45001    4.6     https://vulners.com/exploitdb/EDB-ID:45001      *EXPLOIT*
|       EDB-ID:45000    4.6     https://vulners.com/exploitdb/EDB-ID:45000      *EXPLOIT*
|       EDB-ID:40963    4.6     https://vulners.com/exploitdb/EDB-ID:40963      *EXPLOIT*
|_      EDB-ID:40962    4.6     https://vulners.com/exploitdb/EDB-ID:40962      *EXPLOIT*
80/tcp open  http    Apache httpd 2.2.16 ((Debian))
|_http-server-header: Apache/2.2.16 (Debian)
| vulners: 
|   cpe:/a:apache:http_server:2.2.16: 
|       SSV:72403       7.8     https://vulners.com/seebug/SSV:72403    *EXPLOIT*
|       SSV:26043       7.8     https://vulners.com/seebug/SSV:26043    *EXPLOIT*
|       SSV:20899       7.8     https://vulners.com/seebug/SSV:20899    *EXPLOIT*
|       PACKETSTORM:126851      7.8     https://vulners.com/packetstorm/PACKETSTORM:126851      *EXPLOIT*
|       PACKETSTORM:123527      7.8     https://vulners.com/packetstorm/PACKETSTORM:123527      *EXPLOIT*
|       PACKETSTORM:122962      7.8     https://vulners.com/packetstorm/PACKETSTORM:122962      *EXPLOIT*
|       MSF:AUXILIARY/DOS/HTTP/APACHE_RANGE_DOS 7.8     https://vulners.com/metasploit/MSF:AUXILIARY/DOS/HTTP/APACHE_RANGE_DOS  *EXPLOIT*
|       EXPLOITPACK:186B5FCF5C57B52642E62C06BABC6F83    7.8     https://vulners.com/exploitpack/EXPLOITPACK:186B5FCF5C57B52642E62C06BABC6F83    *EXPLOIT*
|       EDB-ID:18221    7.8     https://vulners.com/exploitdb/EDB-ID:18221      *EXPLOIT*
|       EDB-ID:17696    7.8     https://vulners.com/exploitdb/EDB-ID:17696      *EXPLOIT*
|       CVE-2011-3192   7.8     https://vulners.com/cve/CVE-2011-3192
|       1337DAY-ID-21170        7.8     https://vulners.com/zdt/1337DAY-ID-21170        *EXPLOIT*
|       SSV:60913       7.5     https://vulners.com/seebug/SSV:60913    *EXPLOIT*
|       CVE-2017-7679   7.5     https://vulners.com/cve/CVE-2017-7679
|       CVE-2017-7668   7.5     https://vulners.com/cve/CVE-2017-7668
|       CVE-2017-3169   7.5     https://vulners.com/cve/CVE-2017-3169
|       CVE-2017-3167   7.5     https://vulners.com/cve/CVE-2017-3167
|       CVE-2013-2249   7.5     https://vulners.com/cve/CVE-2013-2249
|       SSV:60427       6.9     https://vulners.com/seebug/SSV:60427    *EXPLOIT*
|       SSV:60386       6.9     https://vulners.com/seebug/SSV:60386    *EXPLOIT*
|       SSV:60069       6.9     https://vulners.com/seebug/SSV:60069    *EXPLOIT*
|       SSV:60788       5.1     https://vulners.com/seebug/SSV:60788    *EXPLOIT*
|       SSV:96537       5.0     https://vulners.com/seebug/SSV:96537    *EXPLOIT*
|       SSV:61874       5.0     https://vulners.com/seebug/SSV:61874    *EXPLOIT*
|       SSV:20993       5.0     https://vulners.com/seebug/SSV:20993    *EXPLOIT*
|       SSV:20979       5.0     https://vulners.com/seebug/SSV:20979    *EXPLOIT*
|       SSV:20969       5.0     https://vulners.com/seebug/SSV:20969    *EXPLOIT*
|       PACKETSTORM:105672      5.0     https://vulners.com/packetstorm/PACKETSTORM:105672      *EXPLOIT*
|       PACKETSTORM:105591      5.0     https://vulners.com/packetstorm/PACKETSTORM:105591      *EXPLOIT*
|       MSF:AUXILIARY/SCANNER/HTTP/REWRITE_PROXY_BYPASS 5.0     https://vulners.com/metasploit/MSF:AUXILIARY/SCANNER/HTTP/REWRITE_PROXY_BYPASS  *EXPLOIT*
|       MSF:AUXILIARY/SCANNER/HTTP/APACHE_OPTIONSBLEED  5.0     https://vulners.com/metasploit/MSF:AUXILIARY/SCANNER/HTTP/APACHE_OPTIONSBLEED   *EXPLOIT*
|       EXPLOITPACK:C8C256BE0BFF5FE1C0405CB0AA9C075D    5.0     https://vulners.com/exploitpack/EXPLOITPACK:C8C256BE0BFF5FE1C0405CB0AA9C075D    *EXPLOIT*
|       EXPLOITPACK:460143F0ACAE117DD79BD75EDFDA154B    5.0     https://vulners.com/exploitpack/EXPLOITPACK:460143F0ACAE117DD79BD75EDFDA154B    *EXPLOIT*
|       EDB-ID:17969    5.0     https://vulners.com/exploitdb/EDB-ID:17969      *EXPLOIT*
|       1337DAY-ID-28573        5.0     https://vulners.com/zdt/1337DAY-ID-28573        *EXPLOIT*
|       SSV:30024       4.6     https://vulners.com/seebug/SSV:30024    *EXPLOIT*
|       EDB-ID:41768    4.6     https://vulners.com/exploitdb/EDB-ID:41768      *EXPLOIT*
|       1337DAY-ID-27465        4.6     https://vulners.com/zdt/1337DAY-ID-27465        *EXPLOIT*
|       SSV:23169       4.4     https://vulners.com/seebug/SSV:23169    *EXPLOIT*
|       EDB-ID:41769    4.4     https://vulners.com/exploitdb/EDB-ID:41769      *EXPLOIT*
|       1337DAY-ID-27473        4.4     https://vulners.com/zdt/1337DAY-ID-27473        *EXPLOIT*
|       SSV:60905       4.3     https://vulners.com/seebug/SSV:60905    *EXPLOIT*
|       SSV:60657       4.3     https://vulners.com/seebug/SSV:60657    *EXPLOIT*
|       SSV:60653       4.3     https://vulners.com/seebug/SSV:60653    *EXPLOIT*
|       SSV:60345       4.3     https://vulners.com/seebug/SSV:60345    *EXPLOIT*
|       SSV:30094       4.3     https://vulners.com/seebug/SSV:30094    *EXPLOIT*
|       SSV:30056       4.3     https://vulners.com/seebug/SSV:30056    *EXPLOIT*
|       SSV:24250       4.3     https://vulners.com/seebug/SSV:24250    *EXPLOIT*
|       SSV:20934       4.3     https://vulners.com/seebug/SSV:20934    *EXPLOIT*
|       SSV:20555       4.3     https://vulners.com/seebug/SSV:20555    *EXPLOIT*
|       PACKETSTORM:109284      4.3     https://vulners.com/packetstorm/PACKETSTORM:109284      *EXPLOIT*
|       EXPLOITPACK:FDCB3D93694E48CD5EE27CE55D6801DE    4.3     https://vulners.com/exploitpack/EXPLOITPACK:FDCB3D93694E48CD5EE27CE55D6801DE    *EXPLOIT*
|       EDB-ID:36663    4.3     https://vulners.com/exploitdb/EDB-ID:36663      *EXPLOIT*
|       EDB-ID:36352    4.3     https://vulners.com/exploitdb/EDB-ID:36352      *EXPLOIT*
|       EDB-ID:35738    4.3     https://vulners.com/exploitdb/EDB-ID:35738      *EXPLOIT*
|       EDB-ID:18442    4.3     https://vulners.com/exploitdb/EDB-ID:18442      *EXPLOIT*
|       SSV:60250       1.2     https://vulners.com/seebug/SSV:60250    *EXPLOIT*
|       EDB-ID:42745    0.0     https://vulners.com/exploitdb/EDB-ID:42745      *EXPLOIT*
|       1337DAY-ID-7972 0.0     https://vulners.com/zdt/1337DAY-ID-7972 *EXPLOIT*
|       1337DAY-ID-23169        0.0     https://vulners.com/zdt/1337DAY-ID-23169        *EXPLOIT*
|_      1337DAY-ID-12139        0.0     https://vulners.com/zdt/1337DAY-ID-12139        *EXPLOIT*
MAC Address: 00:0C:29:AD:E5:A2 (VMware)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.44 seconds


Running Vuln scan on basic ports
                                                                                                                                                                           
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-30 05:28 EST
Nmap scan report for 192.168.110.140
Host is up (0.00069s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 5.5p1 Debian 6+squeeze3 (protocol 2.0)
| vulners: 
|   cpe:/a:openbsd:openssh:5.5p1: 
|       EDB-ID:40888    7.8     https://vulners.com/exploitdb/EDB-ID:40888      *EXPLOIT*
|       CVE-2010-4478   7.5     https://vulners.com/cve/CVE-2010-4478
|       EDB-ID:41173    7.2     https://vulners.com/exploitdb/EDB-ID:41173      *EXPLOIT*
|       SSV:60656       5.0     https://vulners.com/seebug/SSV:60656    *EXPLOIT*
|       CVE-2017-15906  5.0     https://vulners.com/cve/CVE-2017-15906
|       CVE-2010-5107   5.0     https://vulners.com/cve/CVE-2010-5107
|       SSV:90447       4.6     https://vulners.com/seebug/SSV:90447    *EXPLOIT*
|       EDB-ID:45233    4.6     https://vulners.com/exploitdb/EDB-ID:45233      *EXPLOIT*
|       EDB-ID:45210    4.6     https://vulners.com/exploitdb/EDB-ID:45210      *EXPLOIT*
|       EDB-ID:45001    4.6     https://vulners.com/exploitdb/EDB-ID:45001      *EXPLOIT*
|       EDB-ID:45000    4.6     https://vulners.com/exploitdb/EDB-ID:45000      *EXPLOIT*
|       EDB-ID:40963    4.6     https://vulners.com/exploitdb/EDB-ID:40963      *EXPLOIT*
|       EDB-ID:40962    4.6     https://vulners.com/exploitdb/EDB-ID:40962      *EXPLOIT*
|       CVE-2016-0778   4.6     https://vulners.com/cve/CVE-2016-0778
|       CVE-2016-0777   4.0     https://vulners.com/cve/CVE-2016-0777
|       CVE-2012-0814   3.5     https://vulners.com/cve/CVE-2012-0814
|       CVE-2011-5000   3.5     https://vulners.com/cve/CVE-2011-5000
|_      CVE-2011-4327   2.1     https://vulners.com/cve/CVE-2011-4327
80/tcp open  http    Apache httpd 2.2.16 ((Debian))
| http-csrf: 
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=192.168.110.140
|   Found the following possible CSRF vulnerabilities: 
|     
|     Path: http://192.168.110.140:80/examples/servlets/servlet/RequestParamExample
|     Form id: 
|     Form action: RequestParamExample
|     
|     Path: http://192.168.110.140:80/examples/servlets/servlet/SessionExample
|     Form id: 
|     Form action: SessionExample;jsessionid=B5C41EB5E0C752B2F60AC87121DE9CE4
|     
|     Path: http://192.168.110.140:80/examples/servlets/servlet/SessionExample
|     Form id: 
|     Form action: SessionExample;jsessionid=B5C41EB5E0C752B2F60AC87121DE9CE4
|     
|     Path: http://192.168.110.140:80/examples/servlets/servlet/CookieExample
|     Form id: 
|     Form action: CookieExample
|     
|     Path: http://192.168.110.140:80/examples/jsp/checkbox/check.html
|     Form id: 
|_    Form action: checkresult.jsp
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-enum: 
|   /examples/: Sample scripts
|_  /icons/: Potentially interesting folder w/ directory listing
|_http-server-header: Apache/2.2.16 (Debian)
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
| vulners: 
|   cpe:/a:apache:http_server:2.2.16: 
|       SSV:72403       7.8     https://vulners.com/seebug/SSV:72403    *EXPLOIT*
|       SSV:26043       7.8     https://vulners.com/seebug/SSV:26043    *EXPLOIT*
|       SSV:20899       7.8     https://vulners.com/seebug/SSV:20899    *EXPLOIT*
|       PACKETSTORM:126851      7.8     https://vulners.com/packetstorm/PACKETSTORM:126851      *EXPLOIT*
|       PACKETSTORM:123527      7.8     https://vulners.com/packetstorm/PACKETSTORM:123527      *EXPLOIT*
|       PACKETSTORM:122962      7.8     https://vulners.com/packetstorm/PACKETSTORM:122962      *EXPLOIT*
|       MSF:AUXILIARY/DOS/HTTP/APACHE_RANGE_DOS 7.8     https://vulners.com/metasploit/MSF:AUXILIARY/DOS/HTTP/APACHE_RANGE_DOS  *EXPLOIT*
|       EXPLOITPACK:186B5FCF5C57B52642E62C06BABC6F83    7.8     https://vulners.com/exploitpack/EXPLOITPACK:186B5FCF5C57B52642E62C06BABC6F83    *EXPLOIT*
|       EDB-ID:18221    7.8     https://vulners.com/exploitdb/EDB-ID:18221      *EXPLOIT*
|       EDB-ID:17696    7.8     https://vulners.com/exploitdb/EDB-ID:17696      *EXPLOIT*
|       CVE-2011-3192   7.8     https://vulners.com/cve/CVE-2011-3192
|       1337DAY-ID-21170        7.8     https://vulners.com/zdt/1337DAY-ID-21170        *EXPLOIT*
|       SSV:60913       7.5     https://vulners.com/seebug/SSV:60913    *EXPLOIT*
|       CVE-2017-7679   7.5     https://vulners.com/cve/CVE-2017-7679
|       CVE-2017-7668   7.5     https://vulners.com/cve/CVE-2017-7668
|       CVE-2017-3169   7.5     https://vulners.com/cve/CVE-2017-3169
|       CVE-2017-3167   7.5     https://vulners.com/cve/CVE-2017-3167
|       CVE-2013-2249   7.5     https://vulners.com/cve/CVE-2013-2249
|       SSV:60427       6.9     https://vulners.com/seebug/SSV:60427    *EXPLOIT*
|       SSV:60386       6.9     https://vulners.com/seebug/SSV:60386    *EXPLOIT*
|       SSV:60069       6.9     https://vulners.com/seebug/SSV:60069    *EXPLOIT*
|       CVE-2012-0883   6.9     https://vulners.com/cve/CVE-2012-0883
|       CVE-2018-1312   6.8     https://vulners.com/cve/CVE-2018-1312
|       CVE-2017-9788   6.4     https://vulners.com/cve/CVE-2017-9788
|       SSV:60788       5.1     https://vulners.com/seebug/SSV:60788    *EXPLOIT*
|       CVE-2013-1862   5.1     https://vulners.com/cve/CVE-2013-1862
|       SSV:96537       5.0     https://vulners.com/seebug/SSV:96537    *EXPLOIT*
|       SSV:61874       5.0     https://vulners.com/seebug/SSV:61874    *EXPLOIT*
|       SSV:20993       5.0     https://vulners.com/seebug/SSV:20993    *EXPLOIT*
|       SSV:20979       5.0     https://vulners.com/seebug/SSV:20979    *EXPLOIT*
|       SSV:20969       5.0     https://vulners.com/seebug/SSV:20969    *EXPLOIT*
|       PACKETSTORM:105672      5.0     https://vulners.com/packetstorm/PACKETSTORM:105672      *EXPLOIT*
|       PACKETSTORM:105591      5.0     https://vulners.com/packetstorm/PACKETSTORM:105591      *EXPLOIT*
|       MSF:AUXILIARY/SCANNER/HTTP/REWRITE_PROXY_BYPASS 5.0     https://vulners.com/metasploit/MSF:AUXILIARY/SCANNER/HTTP/REWRITE_PROXY_BYPASS  *EXPLOIT*
|       MSF:AUXILIARY/SCANNER/HTTP/APACHE_OPTIONSBLEED  5.0     https://vulners.com/metasploit/MSF:AUXILIARY/SCANNER/HTTP/APACHE_OPTIONSBLEED   *EXPLOIT*
|       EXPLOITPACK:C8C256BE0BFF5FE1C0405CB0AA9C075D    5.0     https://vulners.com/exploitpack/EXPLOITPACK:C8C256BE0BFF5FE1C0405CB0AA9C075D    *EXPLOIT*
|       EXPLOITPACK:460143F0ACAE117DD79BD75EDFDA154B    5.0     https://vulners.com/exploitpack/EXPLOITPACK:460143F0ACAE117DD79BD75EDFDA154B    *EXPLOIT*
|       EDB-ID:17969    5.0     https://vulners.com/exploitdb/EDB-ID:17969      *EXPLOIT*
|       CVE-2017-9798   5.0     https://vulners.com/cve/CVE-2017-9798
|       CVE-2014-0231   5.0     https://vulners.com/cve/CVE-2014-0231
|       CVE-2014-0098   5.0     https://vulners.com/cve/CVE-2014-0098
|       CVE-2013-6438   5.0     https://vulners.com/cve/CVE-2013-6438
|       CVE-2012-4557   5.0     https://vulners.com/cve/CVE-2012-4557
|       CVE-2011-3368   5.0     https://vulners.com/cve/CVE-2011-3368
|       1337DAY-ID-28573        5.0     https://vulners.com/zdt/1337DAY-ID-28573        *EXPLOIT*
|       SSV:30024       4.6     https://vulners.com/seebug/SSV:30024    *EXPLOIT*
|       EDB-ID:41768    4.6     https://vulners.com/exploitdb/EDB-ID:41768      *EXPLOIT*
|       CVE-2012-0031   4.6     https://vulners.com/cve/CVE-2012-0031
|       1337DAY-ID-27465        4.6     https://vulners.com/zdt/1337DAY-ID-27465        *EXPLOIT*
|       SSV:23169       4.4     https://vulners.com/seebug/SSV:23169    *EXPLOIT*
|       EDB-ID:41769    4.4     https://vulners.com/exploitdb/EDB-ID:41769      *EXPLOIT*
|       CVE-2011-3607   4.4     https://vulners.com/cve/CVE-2011-3607
|       1337DAY-ID-27473        4.4     https://vulners.com/zdt/1337DAY-ID-27473        *EXPLOIT*
|       SSV:60905       4.3     https://vulners.com/seebug/SSV:60905    *EXPLOIT*
|       SSV:60657       4.3     https://vulners.com/seebug/SSV:60657    *EXPLOIT*
|       SSV:60653       4.3     https://vulners.com/seebug/SSV:60653    *EXPLOIT*
|       SSV:60345       4.3     https://vulners.com/seebug/SSV:60345    *EXPLOIT*
|       SSV:30094       4.3     https://vulners.com/seebug/SSV:30094    *EXPLOIT*
|       SSV:30056       4.3     https://vulners.com/seebug/SSV:30056    *EXPLOIT*
|       SSV:24250       4.3     https://vulners.com/seebug/SSV:24250    *EXPLOIT*
|       SSV:20934       4.3     https://vulners.com/seebug/SSV:20934    *EXPLOIT*
|       SSV:20555       4.3     https://vulners.com/seebug/SSV:20555    *EXPLOIT*
|       PACKETSTORM:109284      4.3     https://vulners.com/packetstorm/PACKETSTORM:109284      *EXPLOIT*
|       EXPLOITPACK:FDCB3D93694E48CD5EE27CE55D6801DE    4.3     https://vulners.com/exploitpack/EXPLOITPACK:FDCB3D93694E48CD5EE27CE55D6801DE    *EXPLOIT*
|       EDB-ID:36663    4.3     https://vulners.com/exploitdb/EDB-ID:36663      *EXPLOIT*
|       EDB-ID:36352    4.3     https://vulners.com/exploitdb/EDB-ID:36352      *EXPLOIT*
|       EDB-ID:35738    4.3     https://vulners.com/exploitdb/EDB-ID:35738      *EXPLOIT*
|       EDB-ID:18442    4.3     https://vulners.com/exploitdb/EDB-ID:18442      *EXPLOIT*
|       CVE-2016-4975   4.3     https://vulners.com/cve/CVE-2016-4975
|       CVE-2013-1896   4.3     https://vulners.com/cve/CVE-2013-1896
|       CVE-2012-4558   4.3     https://vulners.com/cve/CVE-2012-4558
|       CVE-2012-3499   4.3     https://vulners.com/cve/CVE-2012-3499
|       CVE-2012-0053   4.3     https://vulners.com/cve/CVE-2012-0053
|       CVE-2011-4317   4.3     https://vulners.com/cve/CVE-2011-4317
|       CVE-2011-3639   4.3     https://vulners.com/cve/CVE-2011-3639
|       CVE-2011-3348   4.3     https://vulners.com/cve/CVE-2011-3348
|       CVE-2011-0419   4.3     https://vulners.com/cve/CVE-2011-0419
|       CVE-2012-2687   2.6     https://vulners.com/cve/CVE-2012-2687
|       SSV:60250       1.2     https://vulners.com/seebug/SSV:60250    *EXPLOIT*
|       CVE-2011-4415   1.2     https://vulners.com/cve/CVE-2011-4415
|       EDB-ID:42745    0.0     https://vulners.com/exploitdb/EDB-ID:42745      *EXPLOIT*
|       1337DAY-ID-7972 0.0     https://vulners.com/zdt/1337DAY-ID-7972 *EXPLOIT*
|       1337DAY-ID-23169        0.0     https://vulners.com/zdt/1337DAY-ID-23169        *EXPLOIT*
|_      1337DAY-ID-12139        0.0     https://vulners.com/zdt/1337DAY-ID-12139        *EXPLOIT*
MAC Address: 00:0C:29:AD:E5:A2 (VMware)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 38.97 seconds



---------------------Recon Recommendations----------------------
                                                                                                                                                                           

Web Servers Recon:
                                                                                                                                                                           
gobuster dir -w /usr/share/wordlists/dirb/common.txt -l -t 30 -e -k -x .html,.php -u http://192.168.110.140:80 -o recon/gobuster_192.168.110.140_80.txt
nikto -host 192.168.110.140:80 | tee recon/nikto_192.168.110.140_80.txt





Which commands would you like to run?                                                                                                                                      
All (Default), gobuster, nikto, Skip <!>

Running Default in (1) s:  


---------------------Running Recon Commands----------------------
                                                                                                                                                                           

Starting gobuster scan
                                                                                                                                                                           
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://192.168.110.140:80
[+] Threads:        30
[+] Wordlist:       /usr/share/wordlists/dirb/common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Show length:    true
[+] Extensions:     html,php
[+] Expanded:       true
[+] Timeout:        10s
===============================================================
2021/01/30 05:29:23 Starting gobuster
===============================================================
http://192.168.110.140:80/.htaccess (Status: 403) [Size: 292]
http://192.168.110.140:80/.htaccess.html (Status: 403) [Size: 297]
http://192.168.110.140:80/.htaccess.php (Status: 403) [Size: 296]
http://192.168.110.140:80/.hta (Status: 403) [Size: 287]
http://192.168.110.140:80/.hta.html (Status: 403) [Size: 292]
http://192.168.110.140:80/.hta.php (Status: 403) [Size: 291]
http://192.168.110.140:80/.htpasswd (Status: 403) [Size: 292]
http://192.168.110.140:80/.htpasswd.html (Status: 403) [Size: 297]
http://192.168.110.140:80/.htpasswd.php (Status: 403) [Size: 296]
http://192.168.110.140:80/favicon.ico (Status: 200) [Size: 14634]
http://192.168.110.140:80/index.html (Status: 200) [Size: 320]
http://192.168.110.140:80/index.html (Status: 200) [Size: 320]
http://192.168.110.140:80/server-status (Status: 403) [Size: 296]
===============================================================
2021/01/30 05:29:26 Finished
===============================================================

Finished gobuster scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
Starting nikto scan
                                                                                                                                                                           
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.110.140
+ Target Hostname:    192.168.110.140
+ Target Port:        80
+ Start Time:         2021-01-30 05:29:27 (GMT-5)
---------------------------------------------------------------------------
+ Server: Apache/2.2.16 (Debian)
+ Server may leak inodes via ETags, header found with file /, inode: 3277, size: 320, mtime: Mon Oct  7 15:31:22 2013
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Apache/2.2.16 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS 
+ /examples/servlets/index.html: Apache Tomcat default JSP pages present.
+ Cookie JSESSIONID created without the httponly flag
+ OSVDB-3720: /examples/jsp/snp/snoop.jsp: Displays information about page retrievals, including other users.
+ OSVDB-3268: /icons/: Directory indexing found.
+ OSVDB-3233: /icons/README: Apache default file found.
+ 7915 requests: 0 error(s) and 11 item(s) reported on remote host
+ End Time:           2021-01-30 05:29:51 (GMT-5) (24 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

Finished nikto scan
                                                                                                                                                                           
=========================
                                                                                                                                                                           
                                                                                                                                                                           
                                                                                                                                                                           
---------------------Finished all Nmap scans---------------------                                                                                                          
                                                                                                                                                                           

Completed in 4 minute(s) and 25 second(s)
```