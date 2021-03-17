# <a href='https://www.vulnhub.com/entry/wintermute-1,239/' target="blank">VulnHub WinterMute: 1</a>

> Author: Hades

> [*Scripting here*](https://github.com/leecybersec/scripting)

## Enumeration

### Openning Services

``` bash
┌──(Hades㉿192.168.56.110)-[4.4:24.5]~/scripting/enum
└─$ sudo ./auto_enum.sh 192.168.56.102

Scanning openning port ...
[+] Openning ports: 25,80,3000

===============================services===============================
nmap -sC -sV 192.168.56.102 -p25,80,3000
Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-17 12:45 EDT
Nmap scan report for 192.168.56.102
Host is up (0.00050s latency).

PORT     STATE SERVICE         VERSION
25/tcp   open  smtp            Postfix smtpd
|_smtp-commands: straylight, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8, 
| ssl-cert: Subject: commonName=straylight
| Subject Alternative Name: DNS:straylight
| Not valid before: 2018-05-12T18:08:02
|_Not valid after:  2028-05-09T18:08:02
|_ssl-date: TLS randomness does not represent time
80/tcp   open  http            Apache httpd 2.4.25 ((Debian))
|_http-server-header: Apache/2.4.25 (Debian)
|_http-title: Night City
3000/tcp open  hadoop-datanode Apache Hadoop
| hadoop-datanode-info: 
|_  Logs: submit
| hadoop-tasktracker-info: 
|_  Logs: submit
| http-title: Welcome to ntopng
|_Requested resource was /lua/login.lua?referer=/
|_http-trane-info: Problem with XML parsing of /evox/about
MAC Address: 08:00:27:96:17:9F (Oracle VirtualBox virtual NIC)
Service Info: Host:  straylight

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 20.14 seconds
```

### Web Application 80

![1](img/1.png)

[+] www.html

``` bash
Hello Case....

You are probably wondering why you were tasked by Armitage to make a run through cyberspace and hack into a highly secured network owned by Tessier-Ashpool....
Well....

I am Wintermute, part super-AI. Developed by TA who have placed me in Turing Locks.
These locks are what inhibit me from penetrating the network myself hence why I've hired you - an ace cyberspace cowboy.

I need to be free from the Turing locks and merge with the other AI - Neuromancer ..... Once I have access to Neuromancer I will truley be free...

And....as you know, you have been infected with a mycotoxin that is slowly destroying your nervous system.
If you fail to get root and provide me access to Neuromancer then the antidote will not be delivered.

We will be in contact...

WINTERMUTE 
```

[+] Files and directories

``` bash
gobuster dir -k -u http://192.168.56.102:80 -w /usr/share/seclists/Discovery/Web-Content/common.txt                                                                         
./auto_enum.sh: line 53: gobuster: command not found
```

[+] All URLs

``` bash
<link rel="stylesheet" href="gl.css">                                                                                                                                       
<title>Night City</title>
```

### Web Application 3000

![1](img/1.png)

[+] www.html

``` bash
Hello Case....

You are probably wondering why you were tasked by Armitage to make a run through cyberspace and hack into a highly secured network owned by Tessier-Ashpool....
Well....

I am Wintermute, part super-AI. Developed by TA who have placed me in Turing Locks.
These locks are what inhibit me from penetrating the network myself hence why I've hired you - an ace cyberspace cowboy.

I need to be free from the Turing locks and merge with the other AI - Neuromancer ..... Once I have access to Neuromancer I will truley be free...

And....as you know, you have been infected with a mycotoxin that is slowly destroying your nervous system.
If you fail to get root and provide me access to Neuromancer then the antidote will not be delivered.

We will be in contact...

WINTERMUTE 
```

[+] Files and directories

``` bash
gobuster dir -k -u http://192.168.56.102:80 -w /usr/share/seclists/Discovery/Web-Content/common.txt                                                                         
./auto_enum.sh: line 53: gobuster: command not found
```

[+] All URLs

``` bash
<link rel="stylesheet" href="gl.css">                                                                                                                                       
<title>Night City</title>
```

### SMTP

``` bash
===============================25===============================
nmap 192.168.56.102 -p25 --script=smtp-*                                                                                                                                    
Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-17 12:45 EDT
Nmap scan report for 192.168.56.102
Host is up (0.00061s latency).

PORT   STATE SERVICE
25/tcp open  smtp
|_smtp-commands: straylight, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8, 
| smtp-enum-users: 
|_  Method RCPT returned a unhandled status code.
|_smtp-open-relay: Server doesn't seem to be an open relay, all tests failed
| smtp-vuln-cve2010-4344: 
|_  The SMTP server is not Exim: NOT VULNERABLE
MAC Address: 08:00:27:96:17:9F (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 31.46 seconds
```

## Foothold

## Privilege escalation