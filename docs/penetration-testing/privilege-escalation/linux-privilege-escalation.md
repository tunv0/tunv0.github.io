# Linux Privilege Escalation

## <a href='https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/' target="blank">Basic Linux Privilege Escalation</a>

## <a href='https://gtfobins.github.io/' target="blank">GTFOBins</a>

## Automated Enumeration

``` bash
git clone https://github.com/rebootuser/LinEnum.git

./LinEnum.sh
```

``` bash
git clone https://github.com/diego-treitos/linux-smart-enumeration
```

``` bash
git clone https://github.com/pentestmonkey/unix-privesc-check.git

./unix-privesc-check
./unix-privesc-check standard > output.txt
```

## Upgrade shell

``` bash
/usr/bin/python -c "import pty; pty.spawn('/bin/sh')"
export TERM=xterm

stty raw -echo
fg
```

## <a href='https://www.ssh.com/ssh/tunneling/example' target="blank">Port Tunneling</a>

``` bash
ssh -R $myip:8080:127.0.0.1:8080 kali@$myip
```

## Information Gathering

### What's the OS? What version? What architecture?

``` bash
cat /etc/issue
cat /etc/*-release
uname -i
lsb_release -a (Debian based OSs)
```

### Who are we? Where are we?

``` bash
id
whoami
pwd
```

### Who uses the box? What users? (And which ones have a valid shell)

``` bash
cat /etc/passwd
grep -vE "nologin|false" /etc/passwd
```

### What's currently running on the box? What active network services are there?

``` bash
ps aux
netstat -antup
```

### What's installed? What kernel is being used?

``` bash
dpkg -l (Debian based OSs)
rpm -qa (CentOS / openSUSE )
uname -a
```

## Check sudo access 

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

## Check Scheduled Tasks

<a href='https://github.com/DominicBreuker/pspy' target="blank">pspy</a>

``` bash
ls -lah /etc/cron*
cat /etc/crontab
```

## Readable/Writable Files and Directories

``` bash
find / -writable -type d 2>/dev/null
```

## Check history, bashrc, backup

``` bash
find / -name *history* 2>/dev/null
find / -name *bashrc* -exec grep passwod {} \; 2>/dev/null
```

## Add Local Admin User

``` bash
net user /add pentest Pass
net localgroup administrators pentest /add
```

## Binaries That AutoElevate

``` bash
find / -perm -1000 -type d 2>/dev/null   # Sticky bit - Only the owner of the directory or the owner of a file can delete or rename here.
find / -perm -g=s -type f 2>/dev/null    # SGID (chmod 2000) - run as the group, not the user who started it.
find / -perm -u=s -type f 2>/dev/null    # SUID (chmod 4000) - run as the owner, not the user who started it.

find / -perm -g=s -o -perm -u=s -type f 2>/dev/null    # SGID or SUID
for i in `locate -r "bin$"`; do find $i \( -perm -4000 -o -perm -2000 \) -type f 2>/dev/null; done    # Looks in 'common' places: /bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin, /usr/local/sbin and any other *bin, for SGID or SUID (Quicker search)

# find starting at root (/), SGID or SUID, not Symbolic links, only 3 folders deep, list with more detail and hide any errors (e.g. permission denied)
find / -perm -g=s -o -perm -4000 ! -type l -maxdepth 3 -exec ls -ld {} \; 2>/dev/null
```

## Unmounted Disks

``` bash
cat /etc/fstab
/bin/lsblk
mount
```

## cat /etc/fstab /bin/lsblk mount

``` bash
lsmod
/sbin/modinfo libata
```