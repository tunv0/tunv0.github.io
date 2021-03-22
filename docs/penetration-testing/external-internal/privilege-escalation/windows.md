# Windows Privilege Escalation

## Enumeration Tools

``` bash
git clone https://github.com/pentestmonkey/windows-privesc-check.git

windows-privesc-check2.exe --dump -G
```

## Information Gathering

### What's the OS? What version? What architecture?

``` bash
systeminfo

systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
```

### Who are we? Where are we?

``` bash
whoami
net user
net user <username>
net localgroup administrators
dir
```

### Who uses the box? What users? (And which ones have a valid shell)

``` bash
whoami /groups
net user
```

### What's currently running on the box? What active network services are there?

``` bash
tasklist /SVC

ipconfig /all
route print
netstat -ano
```

### What's installed? What kernel is being used?

``` bash
dir "C:\Program Files"
dir "C:\Program Files (x86)"

wmic product get name, version, vendor

wmic qfe get Caption, Description, HotFixID, InstalledOn
```

## Enumerating Scheduled Tasks
``` bash
schtasks /query /fo LIST /v
```

## Readable/Writable Files and Directories

``` bash
accesschk.exe -uws "Everyone" "C:\Program Files"
Get-ChildItem "C:\Program Files" -Recurse | Get-ACL | ?{$_.AccessToString -match "Everyone\sAllow\s\sModify"}
```

## Unmounted Disks

``` bash
mountvol
```

## Add Local Admin User

``` bash
net user /add pentest Pass
net localgroup administrators pentest /add
```

## Run CMD as Admin

``` bash
powershell.exe Start-Process cmd.exe -Verb runAs
```

## Binaries That AutoElevate

``` bash
reg query HKLM /f pass /t REG_SZ /s

reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer
reg query HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer
```

## Device Drivers and Kernel Modules

``` bash
powershell

driverquery.exe /v /fo csv | ConvertFrom-CSV | Select-Object 'Display Name', 'Start Mode', Path

Get-WmiObject Win32_PnPSignedDriver | Select-Object DeviceName, DriverVersion, Manufacturer | Where-Object {$_.DeviceName -like "*VMware*"}
```

## Firewall Status and Rules

``` bash
netsh advfirewall show currentprofile
```

``` bash
netsh advfirewall firewall show rule name=all
```