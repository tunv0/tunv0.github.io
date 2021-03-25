# <a href='https://www.vulnhub.com/entry/symfonos-1,322/' target="blank">VulnHub symfonos: 1</a>

> Author: Hades

> [*Scripting here*](https://github.com/leecybersec/scripting)

## Enumeration

### Openning Services

``` bash
┌──(Hades㉿192.168.56.110)-[14.5:21.1]~/scripting
└─$ sudo ./enum/auto_enum.sh 192.168.56.109
[sudo] password for kali: 

Scanning openning port ...
[+] Openning ports: 22,25,80,139,445

===============================services===============================
nmap -sC -sV -Pn 192.168.56.109 -p22,25,80,139,445
Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-24 01:08 EDT
Nmap scan report for symfonos.local (192.168.56.109)
Host is up (0.00092s latency).

PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.4p1 Debian 10+deb9u6 (protocol 2.0)
| ssh-hostkey: 
|   2048 ab:5b:45:a7:05:47:a5:04:45:ca:6f:18:bd:18:03:c2 (RSA)
|   256 a0:5f:40:0a:0a:1f:68:35:3e:f4:54:07:61:9f:c6:4a (ECDSA)
|_  256 bc:31:f5:40:bc:08:58:4b:fb:66:17:ff:84:12:ac:1d (ED25519)
25/tcp  open  smtp        Postfix smtpd
|_smtp-commands: symfonos.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8, 
| ssl-cert: Subject: commonName=symfonos
| Subject Alternative Name: DNS:symfonos
| Not valid before: 2019-06-29T00:29:42
|_Not valid after:  2029-06-26T00:29:42
|_ssl-date: TLS randomness does not represent time
80/tcp  open  http        Apache httpd 2.4.25 ((Debian))
|_http-server-header: Apache/2.4.25 (Debian)
|_http-title: Site doesn't have a title (text/html).
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 4.5.16-Debian (workgroup: WORKGROUP)
MAC Address: 08:00:27:7C:ED:13 (Oracle VirtualBox virtual NIC)
Service Info: Hosts:  symfonos.localdomain, SYMFONOS; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 8h39m59s, deviation: 2h53m12s, median: 6h59m59s
|_nbstat: NetBIOS name: SYMFONOS, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.5.16-Debian)
|   Computer name: symfonos
|   NetBIOS computer name: SYMFONOS\x00
|   Domain name: \x00
|   FQDN: symfonos
|_  System time: 2021-03-24T07:08:20-05:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-03-24T12:08:20
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.07 seconds
```

### SMB Service

``` bash
===============================445===============================
smbmap -H 192.168.56.109                                                                                                                                                    
[+] Guest session       IP: 192.168.56.109:445  Name: symfonos.local                                    
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        print$                                                  NO ACCESS       Printer Drivers
        helios                                                  NO ACCESS       Helios personal share
        anonymous                                               READ ONLY
        IPC$                                                    NO ACCESS       IPC Service (Samba 4.5.16-Debian)
smbclient -L 192.168.56.109

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        helios          Disk      Helios personal share
        anonymous       Disk      
        IPC$            IPC       IPC Service (Samba 4.5.16-Debian)
SMB1 disabled -- no workgroup available
```

``` bash
┌──(Hades㉿192.168.56.110)-[6.0:21.9]~/scripting
└─$ smbclient //192.168.56.109/anonymous  
Enter WORKGROUP\kali's password: 
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Fri Jun 28 21:14:49 2019
  ..                                  D        0  Fri Jun 28 21:12:15 2019
  attention.txt                       N      154  Fri Jun 28 21:14:49 2019

                19994224 blocks of size 1024. 17303852 blocks available
smb: \> get attention.txt 
getting file \attention.txt of size 154 as attention.txt (8.4 KiloBytes/sec) (average 8.4 KiloBytes/sec)
smb: \> quit
```

``` bash
┌──(Hades㉿192.168.56.110)-[4.0:21.7]~
└─$ cat attention.txt 

Can users please stop using passwords like 'epidioko', 'qwerty' and 'baseball'! 

Next person I find using one of these passwords will be fired!

-Zeus
```

``` bash
┌──(Hades㉿192.168.56.110)-[3.8:21.7]~
└─$ smbclient //192.168.56.109/helios -U helios                                                                                                                       130 ⨯
Enter WORKGROUP\helios's password: 
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Fri Jun 28 20:32:05 2019
  ..                                  D        0  Fri Jun 28 20:37:04 2019
  research.txt                        A      432  Fri Jun 28 20:32:05 2019
  todo.txt                            A       52  Fri Jun 28 20:32:05 2019

                19994224 blocks of size 1024. 17303852 blocks available
smb: \> get research.txt 
getting file \research.txt of size 432 as research.txt (23.4 KiloBytes/sec) (average 23.4 KiloBytes/sec)
smb: \> get todo.txt 
getting file \todo.txt of size 52 as todo.txt (1.2 KiloBytes/sec) (average 7.6 KiloBytes/sec)
smb: \> quit
```

``` bash
┌──(Hades㉿192.168.56.110)-[3.5:21.7]~
└─$ cat research.txt todo.txt 
Helios (also Helius) was the god of the Sun in Greek mythology. He was thought to ride a golden chariot which brought the Sun across the skies each day from the east (Ethiopia) to the west (Hesperides) while at night he did the return journey in leisurely fashion lounging in a golden cup. The god was famously the subject of the Colossus of Rhodes, the giant bronze statue considered one of the Seven Wonders of the Ancient World.

1. Binge watch Dexter
2. Dance
3. Work on /h3l105
```

## Foothold

## Privilege escalation