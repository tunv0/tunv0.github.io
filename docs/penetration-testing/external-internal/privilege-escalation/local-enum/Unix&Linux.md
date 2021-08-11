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

Set rows and columns

``` bash
stty -a
```

``` bash
stty rows 41 columns 172
```

### Export Terminal

``` bash
export TERM=xterm
```

^Z

``` bash
stty raw -echo; fg
```

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

[How to check if port is in use in](https://www.cyberciti.biz/faq/unix-linux-check-if-port-is-in-use-command/)

``` bash
sudo lsof -i -P -n | grep LISTEN
```

[List all enabled services from systemctl](https://askubuntu.com/questions/795226/how-to-list-all-enabled-services-from-systemctl)

``` bash
systemctl list-unit-files | grep enabled
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
find / -perm -u=s -type f -exec ls -l {} \; 2>/dev/null
```

## Enumeration Tools

<a href='https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/' target="blank">Basic Linux Privilege Escalation</a>

<a href='https://gtfobins.github.io/' target="blank">https://gtfobins.github.io</a>

<a href='https://github.com/DominicBreuker/pspy' target="blank">https://github.com/DominicBreuker/pspy</a>

[https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum)

[https://github.com/diego-treitos/linux-smart-enumeration](https://github.com/diego-treitos/linux-smart-enumeration)

[http://pentestmonkey.net/tools/audit/unix-privesc-check](http://pentestmonkey.net/tools/audit/unix-privesc-check)

## More Commands

### Check history, bashrc, backup

``` bash
find / -name *history* 2>/dev/null
find / -name *bashrc* -exec grep passwod {} \; 2>/dev/null
```

### <a href='https://www.ssh.com/ssh/tunneling/example' target="blank">Port Tunneling</a>

``` bash
ssh -R $myip:8080:127.0.0.1:8080 kali@$myip
```

``` bash
ssh -L 80:ip:80 user@ip
```