# File Transfer

## HTTP Server

### Server

``` bash
sudo python3 -m http.server 80
```

### wget

``` bash
wget <uri> -O /path/to/file.ext

wget <uri> -P /path/to/
```

## SMB Protocol

### Install

``` bash
git clone https://github.com/SecureAuthCorp/impacket.git
cd impacket
sudo pip install -r requirements.txt
sudo python3 setup.py install
```

### SMB Server

``` bash
$ locate whoami.exe
/usr/share/windows-resources/binaries/whoami.exe

$ smbserver.py a /usr/share/windows-binaries/
```

### SMB Server

``` bash
$ \\<ip_server>\a\whoami.exe
```

## FTP Server on Kali Linux

### Install

``` bash
sudo apt-get install vsftpd
sudo service vsftpd start
```

### Anonymous access

``` bash
sudo nano /etc/vsftpd.conf

=> anonymous_enable=YES
```