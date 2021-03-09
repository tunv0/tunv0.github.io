# Basic Commands

## apropos

Search the list of man page descriptions for a possible match based on a keyword.

``` bash
apropos website
get-iab (1)          - Fetch the arp-scan IAB file from the IEEE website
get-oui (1)          - Fetch the arp-scan OUI file from the IEEE website (on Debian and Debian based systems, data is fetched from ieee-data package)
whatweb (1)          - Next generation Web scanner. Identify technologies used by websites.
```

## mkdir

``` bash
mkdir module one

mkdir "module one"

mkdir -p module/{one,two,three}
```

## Piping

``` bash
sudo ss -antlp | grep sshd
```

## sed

``` bash
echo 'Hades' | sed 's/Hades/leecybersec.com/'
```

## cut

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

## awk

``` bash
cat /etc/passwd | awk -F ":" '{print $1, ":", $7}' | grep "sh"
```

## uniq -c

``` bash
cat list.txt | sort | uniq -c | sort -r
```

## Redirect

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

`65`