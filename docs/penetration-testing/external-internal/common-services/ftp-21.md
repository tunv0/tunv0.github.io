# ftp 21

## Check for anonymous access

``` bash
$ ftp $ip $port
Connected to <ip>.
220 Microsoft FTP Service
Name (<ip>:<host>): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password:
230 User logged in.
Remote system type is Windows_NT.
ftp>
```

## FTP Common Commands

``` bash
ftp> passive
Passive mode on.
ftp> binary
200 Type set to I.
ftp> ascii
200 Type set to A.
ftp> upload <file>
ftp> get <file>
ftp> quit
221 Goodbye.
```