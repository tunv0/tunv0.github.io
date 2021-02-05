---
hide:
  - toc        # Hide table of contents
---

# <a href='https://www.hackthebox.eu/home/machines/profile/1' target="blank">Lame</a>

## <a href='https://github.com/rebootuser/LinEnum' target="blank">LinEnum</a>

```
daemon@lame:/tmp$ sh LinEnum.sh
sh LinEnum.sh

#########################################################
# Local Linux Enumeration & Privilege Escalation Script #
#########################################################
# www.rebootuser.com
# version 0.982

[-] Debug Info
[+] Thorough tests = Disabled


Scan started at:
Fri Feb  5 05:35:05 EST 2021                                                                                                                                               
                                                                                                                                                                           

### SYSTEM ##############################################
[-] Kernel information:
Linux lame 2.6.24-16-server #1 SMP Thu Apr 10 13:58:00 UTC 2008 i686 GNU/Linux


[-] Kernel information (continued):
Linux version 2.6.24-16-server (buildd@palmer) (gcc version 4.2.3 (Ubuntu 4.2.3-2ubuntu7)) #1 SMP Thu Apr 10 13:58:00 UTC 2008


[-] Specific release information:
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=8.04
DISTRIB_CODENAME=hardy
DISTRIB_DESCRIPTION="Ubuntu 8.04"


[-] Hostname:
lame


### USER/GROUP ##########################################
[-] Current user/group info:
uid=1(daemon) gid=1(daemon) groups=1(daemon)


[-] Users that have previously logged onto the system:
Username         Port     From             Latest
root             pts/0    :0.0             Fri Feb  5 05:08:27 -0500 2021
makis            pts/1    192.168.150.100  Tue Mar 14 18:32:04 -0400 2017


[-] Who else is logged on:
 05:35:05 up 27 min,  1 user,  load average: 0.00, 0.00, 0.00
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/0    :0.0             05:08   26:38m  0.00s  0.00s -bash


[-] Group memberships:
uid=0(root) gid=0(root) groups=0(root)
uid=1(daemon) gid=1(daemon) groups=1(daemon)
uid=2(bin) gid=2(bin) groups=2(bin)
uid=3(sys) gid=3(sys) groups=3(sys)
uid=4(sync) gid=65534(nogroup) groups=65534(nogroup)
uid=5(games) gid=60(games) groups=60(games)
uid=6(man) gid=12(man) groups=12(man)
uid=7(lp) gid=7(lp) groups=7(lp)
uid=8(mail) gid=8(mail) groups=8(mail)
uid=9(news) gid=9(news) groups=9(news)
uid=10(uucp) gid=10(uucp) groups=10(uucp)
uid=13(proxy) gid=13(proxy) groups=13(proxy)
uid=33(www-data) gid=33(www-data) groups=33(www-data)
uid=34(backup) gid=34(backup) groups=34(backup)
uid=38(list) gid=38(list) groups=38(list)
uid=39(irc) gid=39(irc) groups=39(irc)
uid=41(gnats) gid=41(gnats) groups=41(gnats)
uid=65534(nobody) gid=65534(nogroup) groups=65534(nogroup)
uid=100(libuuid) gid=101(libuuid) groups=101(libuuid)
uid=101(dhcp) gid=102(dhcp) groups=102(dhcp)
uid=102(syslog) gid=103(syslog) groups=103(syslog)
uid=103(klog) gid=104(klog) groups=104(klog)
uid=104(sshd) gid=65534(nogroup) groups=65534(nogroup)
uid=105(bind) gid=113(bind) groups=113(bind)
uid=106(postfix) gid=115(postfix) groups=115(postfix)
uid=107(ftp) gid=65534(nogroup) groups=65534(nogroup)
uid=108(postgres) gid=117(postgres) groups=117(postgres),114(ssl-cert)
uid=109(mysql) gid=118(mysql) groups=118(mysql)
uid=110(tomcat55) gid=65534(nogroup) groups=65534(nogroup)
uid=111(distccd) gid=65534(nogroup) groups=65534(nogroup)
uid=1002(service) gid=1002(service) groups=1002(service)
uid=112(telnetd) gid=120(telnetd) groups=120(telnetd),43(utmp)
uid=113(proftpd) gid=65534(nogroup) groups=65534(nogroup)
uid=114(statd) gid=65534(nogroup) groups=65534(nogroup)
uid=115(snmp) gid=65534(nogroup) groups=65534(nogroup)
uid=1003(makis) gid=1003(makis) groups=1003(makis),4(adm),112(admin)


[-] It looks like we have some admin users:
uid=1003(makis) gid=1003(makis) groups=1003(makis),4(adm),112(admin)


[-] Contents of /etc/passwd:
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/sh
sys:x:3:3:sys:/dev:/bin/sh
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
lp:x:7:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
uucp:x:10:10:uucp:/var/spool/uucp:/bin/sh
proxy:x:13:13:proxy:/bin:/bin/sh
www-data:x:33:33:www-data:/var/www:/bin/sh
backup:x:34:34:backup:/var/backups:/bin/sh
list:x:38:38:Mailing List Manager:/var/list:/bin/sh
irc:x:39:39:ircd:/var/run/ircd:/bin/sh
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/bin/sh
nobody:x:65534:65534:nobody:/nonexistent:/bin/sh
libuuid:x:100:101::/var/lib/libuuid:/bin/sh
dhcp:x:101:102::/nonexistent:/bin/false
syslog:x:102:103::/home/syslog:/bin/false
klog:x:103:104::/home/klog:/bin/false
sshd:x:104:65534::/var/run/sshd:/usr/sbin/nologin
bind:x:105:113::/var/cache/bind:/bin/false
postfix:x:106:115::/var/spool/postfix:/bin/false
ftp:x:107:65534::/home/ftp:/bin/false
postgres:x:108:117:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
mysql:x:109:118:MySQL Server,,,:/var/lib/mysql:/bin/false
tomcat55:x:110:65534::/usr/share/tomcat5.5:/bin/false
distccd:x:111:65534::/:/bin/false
service:x:1002:1002:,,,:/home/service:/bin/bash
telnetd:x:112:120::/nonexistent:/bin/false
proftpd:x:113:65534::/var/run/proftpd:/bin/false
statd:x:114:65534::/var/lib/nfs:/bin/false
snmp:x:115:65534::/var/lib/snmp:/bin/false
makis:x:1003:1003::/home/makis:/bin/sh


[-] Super user account(s):
root


[+] We can sudo without supplying a password!
usage: sudo -h | -K | -k | -L | -l | -V | -v
usage: sudo [-bEHPS] [-p prompt] [-u username|#uid] [VAR=value]
            {-i | -s | <command>}
usage: sudo -e [-S] [-p prompt] [-u username|#uid] file ...


[+] Possible sudo pwnage!
file


[-] Accounts that have recently used sudo:
/home/makis/.sudo_as_admin_successful


[+] We can read root's home directory!
total 80K
drwxr-xr-x 13 root root 4.0K Feb  5 05:08 .
drwxr-xr-x 21 root root 4.0K Oct 31 02:33 ..
-rw-------  1 root root  373 Feb  5 05:08 .Xauthority
lrwxrwxrwx  1 root root    9 May 14  2012 .bash_history -> /dev/null
-rw-r--r--  1 root root 2.2K Oct 20  2007 .bashrc
drwx------  3 root root 4.0K May 20  2012 .config
drwx------  2 root root 4.0K May 20  2012 .filezilla
drwxr-xr-x  5 root root 4.0K Feb  5 05:08 .fluxbox
drwx------  2 root root 4.0K May 20  2012 .gconf
drwx------  2 root root 4.0K May 20  2012 .gconfd
drwxr-xr-x  2 root root 4.0K May 20  2012 .gstreamer-0.10
drwx------  4 root root 4.0K May 20  2012 .mozilla
-rw-r--r--  1 root root  141 Oct 20  2007 .profile
drwx------  5 root root 4.0K May 20  2012 .purple
-rwx------  1 root root    4 May 20  2012 .rhosts
drwxr-xr-x  2 root root 4.0K May 20  2012 .ssh
drwx------  2 root root 4.0K Feb  5 05:08 .vnc
drwxr-xr-x  2 root root 4.0K May 20  2012 Desktop
-rwx------  1 root root  401 May 20  2012 reset_logs.sh
-rw-------  1 root root   33 Feb  5 05:08 root.txt
-rw-r--r--  1 root root  118 Feb  5 05:08 vnc.log


[-] Are permissions on /home directories lax:
total 24K
drwxr-xr-x  6 root    root    4.0K Mar 14  2017 .
drwxr-xr-x 21 root    root    4.0K Oct 31 02:33 ..
drwxr-xr-x  2 root    nogroup 4.0K Mar 17  2010 ftp
drwxr-xr-x  2 makis   makis   4.0K Mar 14  2017 makis
drwxr-xr-x  2 service service 4.0K Apr 16  2010 service
drwxr-xr-x  3    1001    1001 4.0K May  7  2010 user


[-] Root is allowed to login via SSH:
PermitRootLogin yes


### ENVIRONMENTAL #######################################
[-] Environment information:
_DISTCC_SAFEGUARD=1
TERM=linux
QUIET=no
PATH=/sbin:/bin:/usr/sbin:/usr/bin
RUNLEVEL=2
runlevel=2
UPSTART_EVENT=runlevel
PWD=/tmp
VERBOSE=no
PREVLEVEL=N
previous=N
SHLVL=6
UPSTART_JOB=rc2
UPSTART_JOB_ID=5
_=/usr/bin/env


[-] Path information:
/sbin:/bin:/usr/sbin:/usr/bin
drwxr-xr-x 2 root root  4096 Oct 31 02:33 /bin
drwxr-xr-x 2 root root  4096 Nov  3 04:40 /sbin
drwxr-xr-x 2 root root 36864 Nov  3 04:40 /usr/bin
drwxr-xr-x 2 root root 12288 Nov  3 04:40 /usr/sbin


[-] Available shells:
# /etc/shells: valid login shells
/bin/csh
/bin/sh
/usr/bin/es
/usr/bin/ksh
/bin/ksh
/usr/bin/rc
/usr/bin/tcsh
/bin/tcsh
/usr/bin/esh
/bin/dash
/bin/bash
/bin/rbash
/usr/bin/screen


[-] Current umask value:
u=rwx,g=rx,o=rx
0022


[-] Password and storage information:
PASS_MAX_DAYS   99999
PASS_MIN_DAYS   0
PASS_WARN_AGE   7


### JOBS/TASKS ##########################################
[-] Cron jobs:
-rw-r--r-- 1 root root  724 Apr  8  2008 /etc/crontab

/etc/cron.d:
total 20
drwxr-xr-x  2 root root 4096 May 14  2012 .
drwxr-xr-x 96 root root 4096 Feb  5 05:08 ..
-rw-r--r--  1 root root  102 Apr  8  2008 .placeholder
-rw-r--r--  1 root root  492 Jan  6  2010 php5
-rw-r--r--  1 root root 1323 Mar 31  2008 postgresql-common

/etc/cron.daily:
total 60
drwxr-xr-x  2 root root 4096 Apr 28  2010 .
drwxr-xr-x 96 root root 4096 Feb  5 05:08 ..
-rw-r--r--  1 root root  102 Apr  8  2008 .placeholder
-rwxr-xr-x  1 root root  633 Feb  1  2008 apache2
-rwxr-xr-x  1 root root 7441 Apr 22  2008 apt
-rwxr-xr-x  1 root root  314 Apr  4  2008 aptitude
-rwxr-xr-x  1 root root  502 Dec 12  2007 bsdmainutils
-rwxr-xr-x  1 root root   89 Jun 19  2006 logrotate
-rwxr-xr-x  1 root root  954 Mar 12  2008 man-db
-rwxr-xr-x  1 root root  183 Mar  8  2008 mlocate
-rwxr-xr-x  1 root root  383 Apr 28  2010 samba
-rwxr-xr-x  1 root root 3295 Apr  8  2008 standard
-rwxr-xr-x  1 root root 1309 Nov 23  2007 sysklogd
-rwxr-xr-x  1 root root  477 Dec  7  2008 tomcat55

/etc/cron.hourly:
total 12
drwxr-xr-x  2 root root 4096 Mar 16  2010 .
drwxr-xr-x 96 root root 4096 Feb  5 05:08 ..
-rw-r--r--  1 root root  102 Apr  8  2008 .placeholder

/etc/cron.monthly:
total 20
drwxr-xr-x  2 root root 4096 Apr 28  2010 .
drwxr-xr-x 96 root root 4096 Feb  5 05:08 ..
-rw-r--r--  1 root root  102 Apr  8  2008 .placeholder
-rwxr-xr-x  1 root root  664 Feb 20  2008 proftpd
-rwxr-xr-x  1 root root  129 Apr  8  2008 standard

/etc/cron.weekly:
total 24
drwxr-xr-x  2 root root 4096 Mar 16  2010 .
drwxr-xr-x 96 root root 4096 Feb  5 05:08 ..
-rw-r--r--  1 root root  102 Apr  8  2008 .placeholder
-rwxr-xr-x  1 root root  528 Mar 12  2008 man-db
-rwxr-xr-x  1 root root 2522 Jan 28  2008 popularity-contest
-rwxr-xr-x  1 root root 1220 Nov 23  2007 sysklogd


[-] Crontab contents:
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user  command
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#


### NETWORKING  ##########################################
[-] Network and IP info:
eth0      Link encap:Ethernet  HWaddr 00:50:56:b9:2c:bd  
          inet addr:10.10.10.3  Bcast:10.10.10.255  Mask:255.255.255.0
          inet6 addr: dead:beef::250:56ff:feb9:2cbd/64 Scope:Global
          inet6 addr: fe80::250:56ff:feb9:2cbd/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:198 errors:0 dropped:0 overruns:0 frame:0
          TX packets:194 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:63550 (62.0 KB)  TX bytes:25794 (25.1 KB)
          Interrupt:19 Base address:0x2024 

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:315 errors:0 dropped:0 overruns:0 frame:0
          TX packets:315 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:130197 (127.1 KB)  TX bytes:130197 (127.1 KB)


[-] ARP history:
? (10.10.10.2) at 00:50:56:B9:45:04 [ether] on eth0                                                                                                                        
                                                                                                                                                                           
                                                                                                                                                                           
[-] Nameserver(s):                                                                                                                                                         
nameserver 8.8.8.8                                                                                                                                                         
                                                                                                                                                                           
                                                                                                                                                                           
[-] Default route:                                                                                                                                                         
default         10.10.10.2      0.0.0.0         UG    100    0        0 eth0                                                                                               
                                                                                                                                                                           
                                                                                                                                                                           
[-] Listening TCP:                                                                                                                                                         
Active Internet connections (only servers)                                                                                                                                 
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:512             0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:513             0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:2049            0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:514             0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:6697            0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:1099            0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:6667            0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:139             0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:5900            0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:50127           0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:6000            0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:8787            0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:8180            0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:1524            0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:42933           0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:21              0.0.0.0:*               LISTEN      -               
tcp        0      0 10.10.10.3:53           0.0.0.0:*               LISTEN      -               
tcp        0      0 127.0.0.1:53            0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:60278           0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:23              0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:5432            0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:25              0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:50777           0.0.0.0:*               LISTEN      -               
tcp        0      0 127.0.0.1:953           0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:445             0.0.0.0:*               LISTEN      -               
tcp6       0      0 :::2121                 :::*                    LISTEN      -               
tcp6       0      0 :::3632                 :::*                    LISTEN      -               
tcp6       0      0 :::53                   :::*                    LISTEN      -               
tcp6       0      0 :::22                   :::*                    LISTEN      -               
tcp6       0      0 :::5432                 :::*                    LISTEN      -               
tcp6       0      0 ::1:953                 :::*                    LISTEN      -               


[-] Listening UDP:
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
udp        0      0 0.0.0.0:2049            0.0.0.0:*                           -               
udp        0      0 10.10.10.3:137          0.0.0.0:*                           -               
udp        0      0 0.0.0.0:137             0.0.0.0:*                           -               
udp        0      0 10.10.10.3:138          0.0.0.0:*                           -               
udp        0      0 0.0.0.0:138             0.0.0.0:*                           -               
udp        0      0 0.0.0.0:55312           0.0.0.0:*                           -               
udp        0      0 127.0.0.1:161           0.0.0.0:*                           -               
udp        0      0 10.10.10.3:53           0.0.0.0:*                           -               
udp        0      0 127.0.0.1:53            0.0.0.0:*                           -               
udp        0      0 0.0.0.0:69              0.0.0.0:*                           -               
udp        0      0 0.0.0.0:36950           0.0.0.0:*                           -               
udp        0      0 0.0.0.0:991             0.0.0.0:*                           -               
udp        0      0 0.0.0.0:54248           0.0.0.0:*                           -               
udp        0      0 0.0.0.0:111             0.0.0.0:*                           -               
udp        0      0 0.0.0.0:42484           0.0.0.0:*                           -               
udp6       0      0 :::53                   :::*                                -               
udp6       0      0 :::54460                :::*                                -               


### SERVICES #############################################
[-] Running processes:
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.3   2844  1696 ?        Ss   05:07   0:00 /sbin/init
root         2  0.0  0.0      0     0 ?        S<   05:07   0:00 [kthreadd]
root         3  0.0  0.0      0     0 ?        S<   05:07   0:00 [migration/0]
root         4  0.0  0.0      0     0 ?        S<   05:07   0:00 [ksoftirqd/0]
root         5  0.0  0.0      0     0 ?        S<   05:07   0:00 [watchdog/0]
root         6  0.0  0.0      0     0 ?        S<   05:07   0:00 [events/0]
root         7  0.0  0.0      0     0 ?        S<   05:07   0:00 [khelper]
root        41  0.0  0.0      0     0 ?        S<   05:07   0:00 [kblockd/0]
root        64  0.0  0.0      0     0 ?        S<   05:07   0:00 [kseriod]
root       181  0.0  0.0      0     0 ?        S    05:07   0:00 [pdflush]
root       182  0.0  0.0      0     0 ?        S    05:07   0:00 [pdflush]
root       183  0.0  0.0      0     0 ?        S<   05:07   0:00 [kswapd0]
root       224  0.0  0.0      0     0 ?        S<   05:07   0:00 [aio/0]
root      1265  0.0  0.0      0     0 ?        S<   05:07   0:00 [ksnapd]
root      1456  0.0  0.0      0     0 ?        S<   05:07   0:00 [ata/0]
root      1459  0.0  0.0      0     0 ?        S<   05:07   0:00 [ata_aux]
root      1466  0.0  0.0      0     0 ?        S<   05:07   0:00 [scsi_eh_0]
root      1472  0.0  0.0      0     0 ?        S<   05:07   0:00 [scsi_eh_1]
root      1485  0.0  0.0      0     0 ?        S<   05:07   0:00 [ksuspend_usbd]
root      1489  0.0  0.0      0     0 ?        S<   05:07   0:00 [khubd]
root      2347  0.0  0.0      0     0 ?        S<   05:07   0:00 [scsi_eh_2]
root      2566  0.0  0.0      0     0 ?        S<   05:07   0:00 [kjournald]
root      2741  0.0  0.1   2240   748 ?        S<s  05:07   0:00 /sbin/udevd --daemon
root      3133  0.0  0.0      0     0 ?        S<   05:07   0:00 [kpsmoused]
root      4120  0.0  0.0      0     0 ?        S<   05:07   0:00 [kjournald]
root      4288  0.0  0.0      0     0 ?        S<   05:07   0:00 [vmmemctl]
root      4437  0.0  0.7   6508  3712 ?        S    05:07   0:00 /usr/sbin/vmtoolsd
root      4468  0.0  1.4  13708  7680 ?        S    05:07   0:00 /usr/lib/vmware-vgauth/VGAuthService -s
daemon    4613  0.0  0.1   1836   520 ?        Ss   05:07   0:00 /sbin/portmap
statd     4631  0.0  0.1   1900   724 ?        Ss   05:07   0:00 /sbin/rpc.statd
root      4637  0.0  0.0      0     0 ?        S<   05:07   0:00 [rpciod/0]
root      4652  0.0  0.1   3648   564 ?        Ss   05:07   0:00 /usr/sbin/rpc.idmapd
root      4882  0.0  0.0   1716   488 tty4     Ss+  05:07   0:00 /sbin/getty 38400 tty4
root      4884  0.0  0.0   1716   492 tty5     Ss+  05:07   0:00 /sbin/getty 38400 tty5
root      4890  0.0  0.0   1716   488 tty2     Ss+  05:07   0:00 /sbin/getty 38400 tty2
root      4893  0.0  0.0   1716   488 tty3     Ss+  05:07   0:00 /sbin/getty 38400 tty3
root      4895  0.0  0.0   1716   492 tty6     Ss+  05:07   0:00 /sbin/getty 38400 tty6
syslog    4933  0.0  0.1   1936   652 ?        Ss   05:07   0:00 /sbin/syslogd -u syslog
root      4984  0.0  0.1   1872   544 ?        S    05:07   0:00 /bin/dd bs 1 if /proc/kmsg of /var/run/klogd/kmsg
klog      4986  0.0  0.4   3284  2132 ?        Ss   05:07   0:00 /sbin/klogd -P /var/run/klogd/kmsg
bind      5011  0.0  1.4  35408  7676 ?        Ssl  05:07   0:00 /usr/sbin/named -u bind
root      5035  0.0  0.1   5312   996 ?        Ss   05:08   0:00 /usr/sbin/sshd
root      5116  0.0  0.2   2768  1304 ?        S    05:08   0:00 /bin/sh /usr/bin/mysqld_safe
mysql     5158  0.0  3.3 127560 17024 ?        Sl   05:08   0:00 /usr/sbin/mysqld --basedir=/usr --datadir=/var/lib/mysql --user=mysql --pid-file=/var/run/mysqld/mysqld.pid --skip-external-locking --port=3306 --socket=/var/run/mysqld/mysqld.sock
root      5160  0.0  0.1   1700   556 ?        S    05:08   0:00 logger -p daemon.err -t mysqld_safe -i -t mysqld
postgres  5239  0.0  0.9  41340  5072 ?        S    05:08   0:01 /usr/lib/postgresql/8.3/bin/postgres -D /var/lib/postgresql/8.3/main -c config_file=/etc/postgresql/8.3/main/postgresql.conf
postgres  5243  0.0  0.2  41340  1380 ?        Ss   05:08   0:00 postgres: writer process                                                                                                    
postgres  5244  0.0  0.2  41340  1192 ?        Ss   05:08   0:00 postgres: wal writer process                                                                                                
postgres  5245  0.0  0.2  41476  1408 ?        Ss   05:08   0:00 postgres: autovacuum launcher process                                                                                       
postgres  5246  0.0  0.2  12660  1156 ?        Ss   05:08   0:00 postgres: stats collector process                                                                                           
daemon    5266  0.0  0.0   2316   424 ?        SNs  05:08   0:00 distccd --daemon --user daemon --allow 0.0.0.0/0
daemon    5267  0.0  0.1   2316   560 ?        SN   05:08   0:00 distccd --daemon --user daemon --allow 0.0.0.0/0
root      5321  0.0  0.0      0     0 ?        S    05:08   0:00 [lockd]
root      5322  0.0  0.0      0     0 ?        S<   05:08   0:00 [nfsd4]
root      5323  0.0  0.0      0     0 ?        S    05:08   0:00 [nfsd]
root      5324  0.0  0.0      0     0 ?        S    05:08   0:00 [nfsd]
root      5325  0.0  0.0      0     0 ?        S    05:08   0:00 [nfsd]
root      5326  0.0  0.0      0     0 ?        S    05:08   0:00 [nfsd]
root      5327  0.0  0.0      0     0 ?        S    05:08   0:00 [nfsd]
root      5328  0.0  0.0      0     0 ?        S    05:08   0:00 [nfsd]
root      5329  0.0  0.0      0     0 ?        S    05:08   0:00 [nfsd]
root      5330  0.0  0.0      0     0 ?        S    05:08   0:00 [nfsd]
root      5334  0.0  0.0   2424   332 ?        Ss   05:08   0:00 /usr/sbin/rpc.mountd
root      5402  0.0  0.3   5412  1728 ?        Ss   05:08   0:00 /usr/lib/postfix/master
postfix   5406  0.0  0.3   5420  1644 ?        S    05:08   0:00 pickup -l -t fifo -u -c
postfix   5408  0.0  0.3   5460  1684 ?        S    05:08   0:00 qmgr -l -t fifo -u
root      5410  0.0  0.2   5388  1188 ?        Ss   05:08   0:00 /usr/sbin/nmbd -D
root      5412  0.0  0.2   7724  1364 ?        Ss   05:08   0:00 /usr/sbin/smbd -D
root      5416  0.0  0.1   7724   812 ?        S    05:08   0:00 /usr/sbin/smbd -D
snmp      5418  0.0  0.7   8488  3760 ?        S    05:08   0:00 /usr/sbin/snmpd -Lsd -Lf /dev/null -u snmp -I -smux -p /var/run/snmpd.pid 127.0.0.1
root      5434  0.0  0.1   2424   860 ?        Ss   05:08   0:00 /usr/sbin/xinetd -pidfile /var/run/xinetd.pid -stayalive -inetd_compat
daemon    5478  0.0  0.1   2316   560 ?        SN   05:08   0:00 distccd --daemon --user daemon --allow 0.0.0.0/0
daemon    5479  0.0  0.1   2316   560 ?        SN   05:08   0:00 distccd --daemon --user daemon --allow 0.0.0.0/0
proftpd   5500  0.0  0.3   9948  1596 ?        Ss   05:08   0:00 proftpd: (accepting connections)
daemon    5516  0.0  0.0   1984   420 ?        Ss   05:08   0:00 /usr/sbin/atd
root      5529  0.0  0.1   2104   900 ?        Ss   05:08   0:00 /usr/sbin/cron
root      5559  0.0  0.0   2052   348 ?        Ss   05:08   0:00 /usr/bin/jsvc -user tomcat55 -cp /usr/share/java/commons-daemon.jar:/usr/share/tomcat5.5/bin/bootstrap.jar -outfile SYSLOG -errfile SYSLOG -pidfile /var/run/tomcat5.5.pid -Djava.awt.headless=true -Xmx128M -Djava.endorsed.dirs=/usr/share/tomcat5.5/common/endorsed -Dcatalina.base=/var/lib/tomcat5.5 -Dcatalina.home=/usr/share/tomcat5.5 -Djava.io.tmpdir=/var/lib/tomcat5.5/temp -Djava.security.manager -Djava.security.policy=/var/lib/tomcat5.5/conf/catalina.policy org.apache.catalina.startup.Bootstrap
root      5560  0.0  0.0   2052   476 ?        S    05:08   0:00 /usr/bin/jsvc -user tomcat55 -cp /usr/share/java/commons-daemon.jar:/usr/share/tomcat5.5/bin/bootstrap.jar -outfile SYSLOG -errfile SYSLOG -pidfile /var/run/tomcat5.5.pid -Djava.awt.headless=true -Xmx128M -Djava.endorsed.dirs=/usr/share/tomcat5.5/common/endorsed -Dcatalina.base=/var/lib/tomcat5.5 -Dcatalina.home=/usr/share/tomcat5.5 -Djava.io.tmpdir=/var/lib/tomcat5.5/temp -Djava.security.manager -Djava.security.policy=/var/lib/tomcat5.5/conf/catalina.policy org.apache.catalina.startup.Bootstrap
tomcat55  5562  0.6 17.2 323028 88812 ?        Sl   05:08   0:10 /usr/bin/jsvc -user tomcat55 -cp /usr/share/java/commons-daemon.jar:/usr/share/tomcat5.5/bin/bootstrap.jar -outfile SYSLOG -errfile SYSLOG -pidfile /var/run/tomcat5.5.pid -Djava.awt.headless=true -Xmx128M -Djava.endorsed.dirs=/usr/share/tomcat5.5/common/endorsed -Dcatalina.base=/var/lib/tomcat5.5 -Dcatalina.home=/usr/share/tomcat5.5 -Djava.io.tmpdir=/var/lib/tomcat5.5/temp -Djava.security.manager -Djava.security.policy=/var/lib/tomcat5.5/conf/catalina.policy org.apache.catalina.startup.Bootstrap
root      5582  0.0  0.4  10596  2556 ?        Ss   05:08   0:00 /usr/sbin/apache2 -k start
www-data  5583  0.0  0.3  10596  1948 ?        S    05:08   0:00 /usr/sbin/apache2 -k start
www-data  5585  0.0  0.3  10596  1948 ?        S    05:08   0:00 /usr/sbin/apache2 -k start
www-data  5587  0.0  0.3  10596  1948 ?        S    05:08   0:00 /usr/sbin/apache2 -k start
www-data  5590  0.0  0.3  10596  1948 ?        S    05:08   0:00 /usr/sbin/apache2 -k start
www-data  5592  0.0  0.3  10596  1948 ?        S    05:08   0:00 /usr/sbin/apache2 -k start
root      5603  0.0  5.1  66344 26472 ?        Sl   05:08   0:00 /usr/bin/rmiregistry
root      5607  0.0  0.4  12208  2572 ?        Sl   05:08   0:00 ruby /usr/sbin/druby_timeserver.rb
root      5616  0.0  0.4   8540  2364 ?        S    05:08   0:00 /usr/bin/unrealircd
root      5621  0.0  0.0   1716   484 tty1     Ss+  05:08   0:00 /sbin/getty 38400 tty1
root      5626  0.0  2.3  13928 12016 ?        S    05:08   0:00 Xtightvnc :0 -desktop X -auth /root/.Xauthority -geometry 1024x768 -depth 24 -rfbwait 120000 -rfbauth /root/.vnc/passwd -rfbport 5900 -fp /usr/X11R6/lib/X11/fonts/Type1/,/usr/X11R6/lib/X11/fonts/Speedo/,/usr/X11R6/lib/X11/fonts/misc/,/usr/X11R6/lib/X11/fonts/75dpi/,/usr/X11R6/lib/X11/fonts/100dpi/,/usr/share/fonts/X11/misc/,/usr/share/fonts/X11/Type1/,/usr/share/fonts/X11/75dpi/,/usr/share/fonts/X11/100dpi/ -co /etc/X11/rgb
root      5630  0.0  0.2   2724  1184 ?        S    05:08   0:00 /bin/sh /root/.vnc/xstartup
root      5633  0.0  0.4   5936  2576 ?        S    05:08   0:00 xterm -geometry 80x24+10+10 -ls -title X Desktop
root      5636  0.0  0.9   8988  4992 ?        S    05:08   0:00 fluxbox
root      5658  0.0  0.2   2852  1544 pts/0    Ss+  05:08   0:00 -bash
daemon    5740  0.0  0.2   3236  1440 ?        SN   05:13   0:00 sh
daemon    5763  0.0  0.4   3960  2472 ?        SN   05:21   0:00 /usr/bin/python -c import pty; pty.spawn('/bin/bash')
daemon    5764  0.0  0.3   3360  1788 pts/1    SNs  05:21   0:00 /bin/bash
daemon    5802  0.0  0.3   3692  1928 pts/1    SN+  05:35   0:00 sh LinEnum.sh
daemon    5803  0.0  0.2   3732  1464 pts/1    RN+  05:35   0:00 sh LinEnum.sh
daemon    5805  0.0  0.0   1712   444 pts/1    SN+  05:35   0:00 tee -a
daemon    6038  0.0  0.2   3732  1320 pts/1    RN+  05:35   0:00 sh LinEnum.sh
daemon    6039  0.0  0.1   2364   932 pts/1    RN+  05:35   0:00 ps aux


[-] Process binaries and associated permissions (from above list):
692K -rwxr-xr-x 1 root root 686K Apr 14  2008 /bin/bash
 48K -rwxr-xr-x 1 root root  48K Apr  4  2008 /bin/dd
   0 lrwxrwxrwx 1 root root    4 Apr 28  2010 /bin/sh -> bash
 16K -rwxr-xr-x 1 root root  15K Apr 14  2008 /sbin/getty
 92K -rwxr-xr-x 1 root root  88K Apr 11  2008 /sbin/init
 24K -rwxr-xr-x 1 root root  23K Nov 23  2007 /sbin/klogd
 16K -rwxr-xr-x 1 root root  15K Dec  3  2007 /sbin/portmap
 40K -rwxr-xr-x 1 root root  39K Dec  2  2008 /sbin/rpc.statd
 32K -rwxr-xr-x 1 root root  32K Nov 23  2007 /sbin/syslogd
 72K -rwxr-xr-x 1 root root  67K Apr 14  2009 /sbin/udevd
 32K -rwxr-xr-x 1 root root  31K May 21  2007 /usr/bin/jsvc
   0 lrwxrwxrwx 1 root root    9 Apr 28  2010 /usr/bin/python -> python2.5
   0 lrwxrwxrwx 1 root root   29 Apr 28  2010 /usr/bin/rmiregistry -> /etc/alternatives/rmiregistry
1.4M -rwx------ 1 root root 1.4M May 20  2012 /usr/bin/unrealircd
 28K -rwxr-xr-x 1 root root  28K Apr 18  2008 /usr/lib/postfix/master
3.5M -rwxr-xr-x 1 root root 3.5M Mar 21  2008 /usr/lib/postgresql/8.3/bin/postgres
   0 lrwxrwxrwx 1 root root   37 Nov  3 04:40 /usr/lib/vmware-vgauth/VGAuthService -> /usr/lib/vmware-tools/bin32/appLoader
348K -rwxr-xr-x 1 root root 341K Mar  9  2010 /usr/sbin/apache2
 16K -rwxr-xr-x 1 root root  16K Feb 20  2007 /usr/sbin/atd
 32K -rwxr-xr-x 1 root root  31K Apr  8  2008 /usr/sbin/cron
7.1M -rwxr-xr-x 1 root root 7.1M Mar 28  2008 /usr/sbin/mysqld
348K -rwxr-xr-x 1 root root 343K Apr  9  2008 /usr/sbin/named
952K -rwxr-xr-x 1 root root 948K Apr 28  2010 /usr/sbin/nmbd
 36K -rwxr-xr-x 1 root root  35K Dec  2  2008 /usr/sbin/rpc.idmapd
 76K -rwxr-xr-x 1 root root  72K Dec  2  2008 /usr/sbin/rpc.mountd
3.0M -rwxr-xr-x 1 root root 3.0M Apr 28  2010 /usr/sbin/smbd
 24K -rwxr-xr-x 1 root root  24K Sep 24  2009 /usr/sbin/snmpd
368K -rwxr-xr-x 1 root root 363K Apr  6  2008 /usr/sbin/sshd
   0 lrwxrwxrwx 1 root root   37 Nov  3 04:40 /usr/sbin/vmtoolsd -> /usr/lib/vmware-tools/sbin32/vmtoolsd
140K -rwxr-xr-x 1 root root 135K Dec  3  2007 /usr/sbin/xinetd


[-] Contents of /etc/inetd.conf:
#<off># netbios-ssn     stream  tcp     nowait  root    /usr/sbin/tcpd  /usr/sbin/smbd
telnet          stream  tcp     nowait  telnetd /usr/sbin/tcpd  /usr/sbin/in.telnetd
#<off># ftp             stream  tcp     nowait  root    /usr/sbin/tcpd  /usr/sbin/in.ftpd
tftp            dgram   udp     wait    nobody  /usr/sbin/tcpd  /usr/sbin/in.tftpd /srv/tftp
shell           stream  tcp     nowait  root    /usr/sbin/tcpd  /usr/sbin/in.rshd
login           stream  tcp     nowait  root    /usr/sbin/tcpd  /usr/sbin/in.rlogind
exec            stream  tcp     nowait  root    /usr/sbin/tcpd  /usr/sbin/in.rexecd
ingreslock stream tcp nowait root /bin/bash bash -i


[-] The related inetd binary permissions:
-rwxr-xr-x 1 root root  8216 Nov 22  2007 /usr/sbin/in.rexecd
-rwxr-xr-x 1 root root 15620 Nov 22  2007 /usr/sbin/in.rlogind
-rwxr-xr-x 1 root root 14684 Nov 22  2007 /usr/sbin/in.rshd
-rwxr-xr-x 1 root root 36504 Dec 17  2006 /usr/sbin/in.telnetd
-rwxr-xr-x 1 root root 11596 Dec 17  2006 /usr/sbin/in.tftpd
-rwxr-xr-x 1 root root  4504 Jul 30  2007 /usr/sbin/tcpd
-rwxr-xr-x 1 root root  4504 Jul 30  2007 /usr/sbin/tcpd


[-] Contents of /etc/xinetd.conf:
# Simple configuration file for xinetd
#
# Some defaults, and include /etc/xinetd.d/

defaults
{

# Please note that you need a log_type line to be able to use log_on_success
# and log_on_failure. The default is the following :
# log_type = SYSLOG daemon info

}

includedir /etc/xinetd.d


[-] /etc/xinetd.d is included in /etc/xinetd.conf - associated binary permissions are listed below:
total 32
drwxr-xr-x  2 root root 4096 May 20  2012 .
drwxr-xr-x 96 root root 4096 Feb  5 05:08 ..
-rw-r--r--  1 root root  798 Dec  3  2007 chargen
-rw-r--r--  1 root root  660 Dec  3  2007 daytime
-rw-r--r--  1 root root  549 Dec  3  2007 discard
-rw-r--r--  1 root root  580 Dec  3  2007 echo
-rw-r--r--  1 root root  727 Dec  3  2007 time
-rw-r--r--  1 root root  576 May 20  2012 vsftpd


[-] /etc/init.d/ binary permissions:
total 420
drwxr-xr-x  2 root root  4096 Nov  3 04:40 .
drwxr-xr-x 96 root root  4096 Feb  5 05:08 ..
-rw-r--r--  1 root root  1335 Apr 19  2008 README
-rwxr-xr-x  1 root root  5736 Feb  1  2008 apache2
-rwxr-xr-x  1 root root  2653 Apr  7  2008 apparmor
-rwxr-xr-x  1 root root   969 Feb 20  2007 atd
-rwxr-xr-x  1 root root  2426 Apr  9  2008 bind9
-rwxr-xr-x  1 root root  3597 Apr 19  2008 bootclean
-rwxr-xr-x  1 root root  2121 Apr 19  2008 bootlogd
-rwxr-xr-x  1 root root  1768 Apr 19  2008 bootmisc.sh
-rwxr-xr-x  1 root root  3454 Apr 19  2008 checkfs.sh
-rwxr-xr-x  1 root root 10602 Apr 19  2008 checkroot.sh
-rwxr-xr-x  1 root root  6355 May 30  2007 console-screen.sh
-rwxr-xr-x  1 root root  1634 Nov 27  2008 console-setup
-rwxr-xr-x  1 root root  1761 Apr  8  2008 cron
-rwxr-xr-x  1 root root   429 May 14  2012 distcc
-rwxr-xr-x  1 root root  1223 Jun 22  2007 dns-clean
-rwxr-xr-x  1 root root  7195 Apr  4  2008 glibc.sh
-rwxr-xr-x  1 root root  1228 Apr 19  2008 halt
-rwxr-xr-x  1 root root   909 Apr 19  2008 hostname.sh
-rwxr-xr-x  1 root root  4521 Apr 14  2008 hwclock.sh
-rwxr-xr-x  1 root root  4528 Apr 14  2008 hwclockfirst.sh
-rwxr-xr-x  1 root root  1376 Nov 27  2008 keyboard-setup
-rwxr-xr-x  1 root root   944 Apr 19  2008 killprocs
-rwxr-xr-x  1 root root  1729 Nov 23  2007 klogd
-rwxr-xr-x  1 root root   748 Jan 23  2006 loopback
-rwxr-xr-x  1 root root  1399 Feb 25  2008 module-init-tools
-rwxr-xr-x  1 root root   596 Apr 19  2008 mountall-bootclean.sh
-rwxr-xr-x  1 root root  2430 Apr 19  2008 mountall.sh
-rwxr-xr-x  1 root root  1465 Apr 19  2008 mountdevsubfs.sh
-rwxr-xr-x  1 root root  1544 Apr 19  2008 mountkernfs.sh
-rwxr-xr-x  1 root root   594 Apr 19  2008 mountnfs-bootclean.sh
-rwxr-xr-x  1 root root  1244 Apr 19  2008 mountoverflowtmp
-rwxr-xr-x  1 root root  3123 Apr 19  2008 mtab.sh
-rwxr-xr-x  1 root root  5755 Mar 27  2008 mysql
-rwxr-xr-x  1 root root  2515 Mar 27  2008 mysql-ndb
-rwxr-xr-x  1 root root  1905 Mar 27  2008 mysql-ndb-mgm
-rwxr-xr-x  1 root root  1772 Dec  3  2007 networking
-rwxr-xr-x  1 root root  5942 Dec  2  2008 nfs-common
-rwxr-xr-x  1 root root  4411 Dec  2  2008 nfs-kernel-server
-rwxr-xr-x  1 root root  2324 Apr 27  2007 openbsd-inetd
-rwxr-xr-x  1 root root  2377 Oct 23  2007 pcmciautils
-rwxr-xr-x  1 root root  1872 Dec  3  2007 portmap
-rwxr-xr-x  1 root root  4202 Apr 18  2008 postfix
-rwxr-xr-x  1 root root  1170 Mar 21  2008 postgresql-8.3
-rwxr-xr-x  1 root root   375 Oct  4  2007 pppd-dns
-rwxr-xr-x  1 root root  1261 Mar 13  2008 procps
-rwxr-xr-x  1 root root  4848 Feb 20  2008 proftpd
-rwxr-xr-x  1 root root  7891 Apr 19  2008 rc
-rwxr-xr-x  1 root root   522 Apr 19  2008 rc.local
-rwxr-xr-x  1 root root   117 Apr 19  2008 rcS
-rwxr-xr-x  1 root root   692 Apr 19  2008 reboot
-rwxr-xr-x  1 root root  1000 Apr 19  2008 rmnologin
-rwxr-xr-x  1 root root  4945 Apr 10  2008 rsync
-rwxr-xr-x  1 root root  1763 May 25  2004 samba
-rwxr-xr-x  1 root root   955 Oct 23  2007 screen-cleanup
-rwxr-xr-x  1 root root  1199 Apr 19  2008 sendsigs
-rwxr-xr-x  1 root root   585 Apr 19  2008 single
-rwxr-xr-x  1 root root  4215 Apr 19  2008 skeleton
-rwxr-xr-x  1 root root  2747 Sep 24  2009 snmpd
-rwxr-xr-x  1 root root  3839 Apr  6  2008 ssh
-rwxr-xr-x  1 root root   510 Apr 19  2008 stop-bootlogd
-rwxr-xr-x  1 root root   647 Apr 19  2008 stop-bootlogd-single
-rwxr-xr-x  1 root root  3343 Nov 23  2007 sysklogd
-rwxr-xr-x  1 root root  6860 Dec  7  2008 tomcat5.5
-rwxr-xr-x  1 root root  2488 Apr 14  2009 udev
-rwxr-xr-x  1 root root   706 Apr 14  2009 udev-finish
-rwxr-xr-x  1 root root  6358 Apr  7  2008 ufw
-rwxr-xr-x  1 root root  4030 Apr 19  2008 umountfs
-rwxr-xr-x  1 root root  1833 Apr 19  2008 umountnfs.sh
-rwxr-xr-x  1 root root  1863 Apr 19  2008 umountroot
-rwxr-xr-x  1 root root  1815 Apr 19  2008 urandom
-rwxr-xr-x  1 root root 44446 Nov  3 04:40 vmware-tools
-rwxr-xr-x  1 root root  2445 Apr 19  2008 waitnfs.sh
-rwxr-xr-x  1 root root  1626 Mar 12  2008 wpa-ifupdown
-rwxr-xr-x  1 root root  1843 May 13  2008 x11-common
-rwxr-xr-x  1 root root  1896 Dec  3  2007 xinetd
-rwxr-xr-x  1 root root   568 Mar 30  2008 xserver-xorg-input-wacom


### SOFTWARE #############################################
[-] Sudo version:
Sudo version 1.6.9p10


[-] MYSQL version:
mysql  Ver 14.12 Distrib 5.0.51a, for debian-linux-gnu (i486) using readline 5.2


[+] We can connect to the local MYSQL service as 'root' and without a password!
mysqladmin  Ver 8.41 Distrib 5.0.51a, for debian-linux-gnu on i486
Copyright (C) 2000-2006 MySQL AB
This software comes with ABSOLUTELY NO WARRANTY. This is free software,
and you are welcome to modify and redistribute it under the GPL license

Server version          5.0.51a-3ubuntu5
Protocol version        10
Connection              Localhost via UNIX socket
UNIX socket             /var/run/mysqld/mysqld.sock
Uptime:                 27 min 26 sec

Threads: 1  Questions: 438  Slow queries: 0  Opens: 419  Flush tables: 1  Open tables: 64  Queries per second avg: 0.266


[-] Postgres version:
psql (PostgreSQL) 8.3.1
contains support for command-line editing


[-] Apache version:
Server version: Apache/2.2.8 (Ubuntu)
Server built:   Mar  9 2010 20:45:36


[-] Apache user configuration:
APACHE_RUN_USER=www-data
APACHE_RUN_GROUP=www-data


### INTERESTING FILES ####################################
[-] Useful file locations:
/bin/nc
/bin/netcat
/usr/bin/wget
/usr/bin/nmap
/usr/bin/gcc
/usr/bin/curl


[-] Installed compilers:
ii  distcc                                2.18.3-4.1ubuntu1                       Simple distributed compiler client and serve
ii  g++                                   4:4.2.3-1ubuntu6                        The GNU C++ compiler
ii  g++-4.2                               4.2.4-1ubuntu4                          The GNU C++ compiler
ii  gcc                                   4:4.2.3-1ubuntu6                        The GNU C compiler
ii  gcc-4.2                               4.2.4-1ubuntu4                          The GNU C compiler
ii  gcj-4.2                               4.2.4-1ubuntu3                          The GNU compiler for Java(TM)
ii  libecj-java                           3.3.0+0728-5                            Eclipse Java compiler (library)
ii  libecj-java-gcj                       3.3.0+0728-5                            Eclipse Java compiler (native library)


[-] Can we read/write sensitive files:
-rw-r--r-- 1 root root 1549 Mar 14  2017 /etc/passwd
-rw-r--r-- 1 root root 784 Mar 14  2017 /etc/group
-rw-r--r-- 1 root root 497 May 13  2012 /etc/profile
-rw-r----- 1 root shadow 1171 Mar 14  2017 /etc/shadow


[-] SUID files:
-rwsr-xr-x 1 root root 63584 Apr 14  2008 /bin/umount
-rwsr-xr-- 1 root fuse 20056 Feb 26  2008 /bin/fusermount
-rwsr-xr-x 1 root root 25540 Apr  2  2008 /bin/su
-rwsr-xr-x 1 root root 81368 Apr 14  2008 /bin/mount
-rwsr-xr-x 1 root root 30856 Dec 10  2007 /bin/ping
-rwsr-xr-x 1 root root 26684 Dec 10  2007 /bin/ping6
-rwsr-xr-x 1 root root 65520 Dec  2  2008 /sbin/mount.nfs
-rwsr-xr-- 1 root dhcp 2960 Apr  2  2008 /lib/dhcp3-client/call-dhclient-script
-rwsr-xr-x 2 root root 107776 Feb 25  2008 /usr/bin/sudoedit
-rwsr-sr-x 1 root root 7460 Jun 25  2008 /usr/bin/X
-rwsr-xr-x 1 root root 8524 Nov 22  2007 /usr/bin/netkit-rsh
-rwsr-xr-x 1 root root 37360 Apr  2  2008 /usr/bin/gpasswd
-rwsr-xr-x 1 root root 12296 Dec 10  2007 /usr/bin/traceroute6.iputils
-rwsr-xr-x 2 root root 107776 Feb 25  2008 /usr/bin/sudo
-rwsr-xr-x 1 root root 12020 Nov 22  2007 /usr/bin/netkit-rlogin
-rwsr-xr-x 1 root root 11048 Dec 10  2007 /usr/bin/arping
-rwsr-sr-x 1 daemon daemon 38464 Feb 20  2007 /usr/bin/at
-rwsr-xr-x 1 root root 19144 Apr  2  2008 /usr/bin/newgrp
-rwsr-xr-x 1 root root 28624 Apr  2  2008 /usr/bin/chfn
-rwsr-xr-x 1 root root 780676 Apr  8  2008 /usr/bin/nmap
-rwsr-xr-x 1 root root 23952 Apr  2  2008 /usr/bin/chsh
-rwsr-xr-x 1 root root 15952 Nov 22  2007 /usr/bin/netkit-rcp
-rwsr-xr-x 1 root root 29104 Apr  2  2008 /usr/bin/passwd
-rwsr-xr-x 1 root root 46084 Mar 31  2008 /usr/bin/mtr
-rwsr-sr-x 1 libuuid libuuid 12336 Mar 27  2008 /usr/sbin/uuidd
-rwsr-xr-- 1 root dip 269256 Oct  4  2007 /usr/sbin/pppd
-rwsr-xr-- 1 root telnetd 6040 Dec 17  2006 /usr/lib/telnetlogin
-rwsr-xr-- 1 root www-data 10276 Mar  9  2010 /usr/lib/apache2/suexec
-rwsr-xr-x 1 root root 4524 Nov  5  2007 /usr/lib/eject/dmcrypt-get-device
-rwsr-xr-x 1 root root 165748 Apr  6  2008 /usr/lib/openssh/ssh-keysign
-rwsr-xr-x 1 root root 9624 Aug 17  2009 /usr/lib/pt_chown
-r-sr-xr-x 1 root root 14320 Nov  3 04:40 /usr/lib/vmware-tools/bin64/vmware-user-suid-wrapper
-r-sr-xr-x 1 root root 9532 Nov  3 04:40 /usr/lib/vmware-tools/bin32/vmware-user-suid-wrapper


[+] Possibly interesting SUID files:
-rwsr-xr-- 1 root dhcp 2960 Apr  2  2008 /lib/dhcp3-client/call-dhclient-script
-rwsr-xr-x 1 root root 780676 Apr  8  2008 /usr/bin/nmap


[-] SGID files:
-rwxr-sr-x 1 root shadow 19584 Apr  9  2008 /sbin/unix_chkpwd
-rwxr-sr-x 1 root utmp 3192 Apr 22  2008 /usr/bin/Eterm
-rwsr-sr-x 1 root root 7460 Jun 25  2008 /usr/bin/X
-rwxr-sr-x 1 root tty 8192 Dec 12  2007 /usr/bin/bsd-write
-rwxr-sr-x 1 root ssh 76580 Apr  6  2008 /usr/bin/ssh-agent
-rwxr-sr-x 1 root mlocate 30508 Mar  8  2008 /usr/bin/mlocate
-rwxr-sr-x 1 root crontab 26928 Apr  8  2008 /usr/bin/crontab
-rwxr-sr-x 1 root shadow 37904 Apr  2  2008 /usr/bin/chage
-rwxr-sr-x 1 root utmp 308228 Oct 23  2007 /usr/bin/screen
-rwxr-sr-x 1 root shadow 16424 Apr  2  2008 /usr/bin/expiry
-rwsr-sr-x 1 daemon daemon 38464 Feb 20  2007 /usr/bin/at
-rwxr-sr-x 1 root utmp 306996 Jan  2  2009 /usr/bin/xterm
-rwxr-sr-x 1 root tty 9960 Apr 14  2008 /usr/bin/wall
-rwsr-sr-x 1 libuuid libuuid 12336 Mar 27  2008 /usr/sbin/uuidd
-r-xr-sr-x 1 root postdrop 10312 Apr 18  2008 /usr/sbin/postqueue
-r-xr-sr-x 1 root postdrop 10036 Apr 18  2008 /usr/sbin/postdrop


[+] Hosts.equiv file and contents: 
-rw-r--r-- 1 root root 121 May 20  2012 /etc/hosts.equiv
# /etc/hosts.equiv: list  of  hosts  and  users  that are granted "trusted" r
#                   command access to your system .
+ +


[-] NFS config details: 
-rw-r--r-- 1 root root 367 May 13  2012 /etc/exports
# /etc/exports: the access control list for filesystems which may be exported
#               to NFS clients.  See exports(5).
#
# Example for NFSv2 and NFSv3:
# /srv/homes       hostname1(rw,sync) hostname2(ro,sync)
#
# Example for NFSv4:
# /srv/nfs4        gss/krb5i(rw,sync,fsid=0,crossmnt)
# /srv/nfs4/homes  gss/krb5i(rw,sync)
#

/       *(rw,sync,no_root_squash,no_subtree_check)


[-] Can't search *.conf files as no keyword was entered

[-] Can't search *.php files as no keyword was entered

[-] Can't search *.log files as no keyword was entered

[-] Can't search *.ini files as no keyword was entered

[-] All *.conf files in /etc (recursive 1 level):
-rw-r--r-- 1 root root 552 Apr  9  2008 /etc/pam.conf
-rw-r--r-- 1 root root 899 Nov  6  2007 /etc/gssapi_mech.conf
-rw-r----- 1 root fuse 216 Feb 26  2008 /etc/fuse.conf
-rw-r--r-- 1 root root 2405 Mar 13  2008 /etc/sysctl.conf
-rw-r--r-- 1 root root 2689 Apr  4  2008 /etc/gai.conf
-rw-r--r-- 1 root root 4430 May 20  2012 /etc/vsftpd.conf
-rw-r--r-- 1 root root 2975 Mar 16  2010 /etc/adduser.conf
-rw-r--r-- 1 root root 2969 Mar 11  2008 /etc/debconf.conf
-rw-r--r-- 1 root root 92 Oct 20  2007 /etc/host.conf
-rw-r--r-- 1 root root 13144 Nov 16  2007 /etc/ltrace.conf
-rw-r--r-- 1 root root 423 May 20  2012 /etc/hesiod.conf
-rw-r--r-- 1 root root 34 Mar 16  2010 /etc/ld.so.conf
-rw-r--r-- 1 root root 599 Jun 19  2006 /etc/logrotate.conf
-rw-r--r-- 1 root root 354 Mar  5  2007 /etc/fdmount.conf
-rw-r--r-- 1 root root 529 May 20  2012 /etc/inetd.conf
-rw-r--r-- 1 root root 475 Oct 20  2007 /etc/nsswitch.conf
-rw-r--r-- 1 root root 214 Mar  8  2008 /etc/updatedb.conf
-rw-r--r-- 1 root root 19 Oct 31 02:13 /etc/resolv.conf
-rw-r--r-- 1 root root 34 Feb 18  2008 /etc/e2fsck.conf
-rw-r--r-- 1 root root 4793 Mar 28  2008 /etc/hdparm.conf
-rw-r--r-- 1 root root 342 Mar 16  2010 /etc/popularity-contest.conf
-rw-r--r-- 1 root root 417 Mar 27  2008 /etc/mke2fs.conf
-rw-r--r-- 1 root root 15280 Apr 28  2010 /etc/devscripts.conf
-rw-r--r-- 1 root root 1614 Nov 23  2007 /etc/syslog.conf
-rw-r--r-- 1 root root 1260 Feb 21  2008 /etc/ucf.conf
-rw-r--r-- 1 root root 145 Dec  2  2008 /etc/idmapd.conf
-rw-r--r-- 1 root root 600 Oct 23  2007 /etc/deluser.conf
-rw-r--r-- 1 root root 240 Mar 16  2010 /etc/kernel-img.conf
-rw-r--r-- 1 root root 1878 May  4  2008 /etc/cowpoke.conf
-rw-r--r-- 1 root root 289 May 20  2012 /etc/xinetd.conf


[+] Root's history files are accessible!
lrwxrwxrwx 1 root root 9 May 14  2012 /root/.bash_history -> /dev/null


[-] Location and contents (if accessible) of .bash_history file(s):
/home/makis/.bash_history
/home/user/.bash_history


[-] Location and Permissions (if accessible) of .bak file(s):
-rw-r--r-- 1 root root 7970844 Oct 31 02:37 /boot/initrd.img-2.6.24-16-server.bak
-rw-r--r-- 1 root root 7969070 Oct 31 02:33 /boot/initrd.img-2.6.24-32-server.bak
-rw------- 1 root shadow 1081 Apr 28  2010 /var/backups/shadow.bak
-rw------- 1 root root 886 Apr 16  2010 /var/backups/group.bak
-rw------- 1 root shadow 742 Apr 16  2010 /var/backups/gshadow.bak
-rw------- 1 root root 1538 Apr 28  2010 /var/backups/passwd.bak
-rw-r--r-- 1 root root 3731 May 20  2012 /var/backups/infodir.bak


[-] Any interesting mail in /var/mail:
total 12
drwxrwsr-x  2 root mail 4096 Mar 14  2017 .
drwxr-xr-x 15 root root 4096 May 20  2012 ..
-rw-------  1 root mail 1438 Mar 14  2017 root


### SCAN COMPLETE ####################################
```