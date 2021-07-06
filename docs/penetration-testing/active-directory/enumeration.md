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

Get Host Name of the Domain Controller

``` bash
[System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()
```

=== "Enum"

	``` bash
	PS C:\Users\admin\Desktop> .\ldap-enum.ps1
	LDAP://WIN-GFL2HT22DPG.leecybersec.com/DC=leecybersec,DC=local

	Name                           Value
	----                           -----
	givenname                      {admin}
	<snip>
	distinguishedname              {CN=admin,CN=Users,DC=leecybersec,DC=local}
	userprincipalname              {admin@leecybersec.local}
	```

=== "ldap-enum.ps1"

	``` bash
	# Generate LDAP path, file `ldap-enum.ps1`

	# .\ldap-enum.ps1
	# LDAP://WIN-GFL2HT22DPG.leecybersec.com/DC=leecybersec,DC=local

	$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()
	$PDC = ($domainObj.PdcRoleOwner).Name
	$SearchString = "LDAP://"
	$SearchString += $PDC + "/"
	$DistinguishedName = "DC=$($domainObj.Name.Replace('.', ',DC='))"
	$SearchString += $DistinguishedName
	$SearchString

	# Execute LDAP search for each user

	$Searcher = New-Object System.DirectoryServices.DirectorySearcher([ADSI]$SearchString)
	$objDomain = New-Object System.DirectoryServices.DirectoryEntry
	$Searcher.SearchRoot = $objDomain

	# supply 0x30000000 (decimal 805306368) to enumerate all users in the domain
	# $Searcher.filter="samAccountType=805306368"

	$Searcher.filter="name=admin"

	$Result = $Searcher.FindAll()

	Foreach($obj in $Result)
	{
		Foreach($prop in $obj.Properties)
		{
			$prop
		}

		Write-Host "------------------------"
	}
	```

## Resolving Nested Groups