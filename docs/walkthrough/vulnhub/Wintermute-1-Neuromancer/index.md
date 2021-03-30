# VulnHub WinterMute: 1 (Neuromancer)

> Author: Hades - [LeeCyberSec](https://leecybersec.com)

> [*Scripting here*](https://github.com/leecybersec/scripting)

## VM Details

|**Name**|WinterMute: 1|
|---|---|
|**Date release**|5 Jul 2018|
|**Author**|[creosote](https://www.vulnhub.com/author/creosote,584/)|
|**Series**|[WinterMute](https://www.vulnhub.com/series/wintermute,161/)|

## Information Gathering

### Openning Services

After get root at [WinterMute: 1 (Straylight)](/walkthrough/vulnhub/Wintermute-1-Straylight/)
I enum the network and saw that there are 2 interfaces `enp0s3` and `enp0s8`.

``` txt
root@straylight:/tmp# ifconfig
enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.56.102  netmask 255.255.255.0  broadcast 192.168.56.255
        <snip>

enp0s8: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.107.106  netmask 255.255.255.0  broadcast 192.168.107.255
        <snip>
<snip>
```

> [*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/vulnhub/wintermute-1-straylight)

``` txt
root@straylight:/tmp# bash pingSweeping.sh 192.168.107
192.168.107.2
192.168.107.1
192.168.107.106
192.168.107.107
```

Scan open port in `192.168.107.107` with `nc`.

``` bash
root@straylight:/tmp# nc -nv -w 1 -z 192.168.107.107 1-65535
(UNKNOWN) [192.168.107.107] 34483 (?) open
(UNKNOWN) [192.168.107.107] 8080 (http-alt) open
(UNKNOWN) [192.168.107.107] 8009 (?) open
```

### Port Tunneling

I used `socat` to redirect port 8080,8009,34483 conenctions to `192.168.107.107`

``` txt
root@straylight:/tmp# socat TCP-LISTEN:8080,fork TCP:192.168.107.107:8080 &
[1] 8283
root@straylight:/tmp# socat TCP-LISTEN:8009,fork TCP:192.168.107.107:8009 &
[2] 8449
root@straylight:/tmp# socat TCP-LISTEN:34483,fork TCP:192.168.107.107:34483 &
[3] 8458
root@straylight:/tmp#
```

### Enum Service

``` txt
┌──(Hades㉿192.168.56.110)-[1.5:39.9]~/scripting
└─$ sudo ./enum/all.sh 192.168.56.102 8080,8009,34483 
[sudo] password for kali: 

### Enum ports from input: 8080,8009,34483

### Services Enumeration ############################
nmap -sC -sV -Pn 192.168.56.102 -p8080,8009,34483
Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-30 12:50 EDT
Nmap scan report for 192.168.56.102
Host is up (0.00054s latency).

PORT      STATE SERVICE VERSION
8009/tcp  open  ajp13   Apache Jserv (Protocol v1.3)
|_ajp-methods: Failed to get a valid response for the OPTION request
8080/tcp  open  http    Apache Tomcat 9.0.0.M26
|_http-favicon: Apache Tomcat
|_http-title: Apache Tomcat/9.0.0.M26
34483/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 2e:9b:4a:a9:c0:fc:0b:d8:ef:f1:e3:9d:f4:59:25:32 (RSA)
|   256 f6:2a:de:07:36:36:00:e9:b5:5d:2f:aa:03:79:91:d1 (ECDSA)
|_  256 38:3c:a8:ed:91:ea:ce:1d:0d:0f:ab:51:ac:97:c8:fb (ED25519)
MAC Address: 08:00:27:0E:1B:0D (Oracle VirtualBox virtual NIC)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 19.89 seconds
```