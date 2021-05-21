# Linux Privilege Escalation

## User Enumeration

Current User

``` bash
whoami
```

``` bash
id
```

Other Users

``` bash
cat /etc/passwd
```

Which ones have a valid shell

``` bash
grep -vE "nologin|false" /etc/passwd
```

Folder

``` bash
pwd; ls -la
```

Hostname

``` bash
hostname
```

## OS Version & Architecture

What's the OS?

``` bash
cat /etc/issue
```

``` bash
cat /etc/*-release
```

``` bash
lsb_release -a (Debian based OSs)
```

Kernel version and Architecture

``` bash
uname -a
```

## Processes and Services

``` bash
ps axu
```

## Networking Enumeration

### Interface and Routable

``` bash
ip a
```

``` bash
/sbin/route
```

### Active network connection

``` bash
ss -anp
```

``` bash
netstat -antup
```

## Firewall and Rules

``` bash
grep -Hs iptables /etc/*
```

## Scheduled Tasks

``` bash
ls -lah /etc/cron*
```

``` bash
cat /etc/crontab
```

``` bash
grep "CRON" /var/log/* 2>/dev/null
```

## Installed and Patch Levels

``` bash
dpkg -l (Debian based OSs)
```

``` bash
rpm -qa (CentOS / openSUSE )
```

``` bash
uname -a
```

## Readable/Writable

``` bash
find / -writable -type d 2>/dev/null
```

## Unmounted Disks

List all mounted files system

``` bash
mount
```

``` bash
cat /etc/fstab
```

List all disk

``` bash
/bin/lsblk
```

Mount disk

``` bash
sudo mount -o nolock 192.168.11.131:/share ~/share
```

## Device Drivers & Kernel Modules

``` bash
lsmod
```

``` bash
/sbin/modinfo <name>
```

## Binaries That AutoElevate

``` bash
find / -perm -1000 -type d 2>/dev/null   # Sticky bit - Only the owner of the directory or the owner of a file can delete or rename here.
```

``` bash
find / -perm -g=s -type f 2>/dev/null    # SGID (chmod 2000) - run as the group, not the user who started it.
find / -perm -u=s -type f 2>/dev/null    # SUID (chmod 4000) - run as the owner, not the user who started it.
```

``` bash
find / -perm -g=s -o -perm -u=s -type f 2>/dev/null    # SGID or SUID
for i in `locate -r "bin$"`; do find $i \( -perm -4000 -o -perm -2000 \) -type f 2>/dev/null; done    # Looks in 'common' places: /bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin, /usr/local/sbin and any other *bin, for SGID or SUID (Quicker search)
```

``` bash
# find starting at root (/), SGID or SUID, not Symbolic links, only 3 folders deep, list with more detail and hide any errors (e.g. permission denied)
find / -perm -g=s -o -perm -4000 ! -type l -maxdepth 3 -exec ls -ld {} \; 2>/dev/null
```

## Enumeration Tools

<a href='https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/' target="blank">Basic Linux Privilege Escalation</a>

<a href='https://gtfobins.github.io/' target="blank">GTFOBins</a>

<a href='https://github.com/DominicBreuker/pspy' target="blank">pspy</a>

[LinEnum.sh](https://github.com/rebootuser/LinEnum)

``` bash
LinEnum.sh
```

[lse.sh](https://github.com/diego-treitos/linux-smart-enumeration)

``` bash
lse.sh
```

[unix-privesc-check](http://pentestmonkey.net/tools/audit/unix-privesc-check)

``` bash
./unix-privesc-check standard
```

## More Reference

### Check sudo access 

``` bash
$ sudo -l
[sudo] password for Hades: 
Matching Defaults entries for pentesterlab on 7358cafc3ebe:
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin
User Hades may run the following commands:
    (victim) /bin/bash
```

Mix cp/chown and chmod

https://www.adampalmer.me/iodigitalsec/2009/10/03/linux-c-setuid-setgid-tutorial/

https://www.hackingarticles.in/linux-privilege-escalation-using-suid-binaries/

``` bash
sudo -l
Matching Defaults entries for Hades:
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin
User Hades may run the following commands:
    (victim) /bin/chmod, /bin/cp
```

### Check history, bashrc, backup

``` bash
find / -name *history* 2>/dev/null
find / -name *bashrc* -exec grep passwod {} \; 2>/dev/null
```

### Checking docker container

``` bash
root@315d7648a173:/# ls -lah
<snip>
-rwxr-xr-x   1 root root    0 Jun  9 13:01 .dockerenv
```

``` bash
mkdir -p /mnt/hola
```

``` bash
mount /dev/sda1 /mnt/hola
mount /dev/sda2 /mnt/hola
mount /dev/sda3 /mnt/hola
```

### <a href='https://www.ssh.com/ssh/tunneling/example' target="blank">Port Tunneling</a>

``` bash
ssh -R $myip:8080:127.0.0.1:8080 kali@$myip
```

``` bash
ssh -L 80:ip:80 user@ip
```