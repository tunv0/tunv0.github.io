# Active Directory Enumeration

## Users and Groups

Users Enumeration

``` bash
net user /domain
```

``` bash
net user hades /domain
```

Group Enumeration

``` bash
net group /domain
```

``` bash
net localgroup administrators
```

## LDAP Enum

``` bash
LDAP://HostName[:PortNumber][/DistinguishedName]
```

Get current domain

`powershell.exe -c`

``` bash
[System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()
```