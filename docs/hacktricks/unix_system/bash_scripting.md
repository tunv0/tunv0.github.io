# Bash Scripting

[https://devhints.io/bash](https://devhints.io/bash)

[https://github.com/leecybersec/bash-script](https://github.com/leecybersec/bash-script)

## Hello World

=== "Running"

	``` bash
	chmod +x hello_world.sh

	./hello_world.sh
	```

=== "hello_world.sh"

	``` bash
	#!/bin/bash

	echo "Hello World!"
	```

## My Self Script

=== "Running"

	``` bash
	chmod +x my_self.sh

	./my_self.sh
	```

=== "my_self.sh"

	``` bash
	#!/bin/bash

	ip="$(ifconfig | grep eth0 -C 1 | grep inet | cut -f10 -d' ')"

	name=`whoami`

	echo "I'm $name"

	echo "My IP is $ip"

	echo "Command: ping -c 2 $ip"

	ping -c 2 $ip

	```

## Arguments and If Else Elif and Boolean

=== "Arguments"

	- `$0` The name of the Bash script
	- `$1 -$9` The first 9 arguments to the Bash script
	- `$#` Number of arguments passed to the Bash script
	- `$@` All arguments passed to the Bash script
	- `$?` The exit status of the most recently run process
	- `$$` The process ID of the current script
	- `$USER` The username of the user running the script
	- `$HOSTNAME` The hostname of the machine
	- `$RANDOM` A random number
	- `$LINENO` The current line number in the script

=== "If Else Elif"

	- `!EXPRESSION` The EXPRESSION is false.
	- `-n STRING` STRING length is greater than zero
	- `-z STRING` The length of STRING is zero (empty)
	- `STRING1 != STRING2` STRING1 is not equal to STRING2
	- `STRING1 = STRING2` STRING1 is equal to STRING2
	- `INTEGER1 -eq INTEGER2` INTEGER1 is equal to INTEGER2
	- `INTEGER1 -ne INTEGER2` INTEGER1 is not equal to INTEGER2
	- `INTEGER1 -gt INTEGER2` INTEGER1 is greater than INTEGER2
	- `INTEGER1 -lt INTEGER2` INTEGER1 is less than INTEGER2
	- `INTEGER1 -ge INTEGER2` INTEGER1 is greater than or equal to INTEGER 2
	- `INTEGER1 -le INTEGER2` INTEGER1 is less than or equal to INTEGER 2
	- `-d FILE` FILE exists and is a directory
	- `-e FILE` FILE exists
	- `-r FILE` FILE exists and has read permission
	- `-s FILE` FILE exists and it is not empty
	- `-w FILE` FILE exists and has write permission
	- `-x FILE` FILE exists and has execute permission

Nmap All Ports Scan Script

=== "Running"

	``` bash
	chmod +x nmap_all_ports.sh

	./nmap_all_ports.sh 127.0.0.1
	```

=== "nmap_all_ports.sh"

	``` bash
	#!/bin/bash

	if [ $# -eq 0 ] || [ $1 = "-h" ] || [ $1 = "--help" ]
	then
		echo "Usage: $0 <HOST>"
		exit
	else
		ports=$(nmap -p- --min-rate 1000 $1 | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//)
		
		if [ -z $ports ]
		then
			echo "No open port!"
			exit
		else
			echo "Opening port: $ports"
			nmap -sC -sV -p $ports $1
		fi
	fi
	```

## Loops and Functions

=== "Loops"

	``` bash
	for var-name in <list>
	do
		<action to perform>
	done
	```

	``` bash
	while [ <some test> ]
	do
		<perform an action>
	done
	```

=== "Functions"

	``` bash
	function function_name 
	{
		commands...
	}
	```

	``` bash
	function_name ()
	{
		commands...
	}
	```

Auto Enum Script

=== "Running"

	``` bash
	chmod +x auto_enum.sh

	./auto_enum.sh 127.0.0.1
	```

=== "auto_enum.sh"

	``` bash
	#!/bin/bash

	RED='\033[0;31m'
	YELLOW='\033[0;33m'
	GREEN='\033[0;32m'
	NC='\033[0m'
	origIFS="${IFS}"

	enum_all_port ()
	{
		echo "nmap -p- --min-rate 1000 $1 | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//"
		
		ports=$(nmap -p- --min-rate 1000 $1 | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//)

		if [ -z $ports ]; then
			printf "${RED}[-]No open port!${NC}"
			exit
		fi
	}

	enum_open_service ()
	{
		echo "nmap -sC -sV -p$2 $1"
		nmap -sC -sV -p$2 $1
	}

	enum_smtp_service ()
	{
		printf "${GREEN}$port\n${NC}"

		echo "nmap $1 -p $2 --script=smtp-*"
		nmap $1 -p $2 --script=smtp-*
	}

	enum_http_service ()
	{
		printf "${GREEN}$port\n${NC}"

		echo "gobuster dir -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://$1:$2"
		gobuster dir -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://$1:$2
	}

	enum_ssmb_service ()
	{
		printf "${GREEN}$port\n${NC}"

		echo "smbmap -H $1"
		smbmap -H $1

		echo "smbclient -L $1"
		smbclient -L $1
	}

	recon ()
	{
		for port in $array_port; do
			if [[ $port = "25" ]]; then
				enum_smtp_service $host $port
			elif [[ $port = "80" ]] || [[ $port = "443" ]]; then
				enum_http_service $host $port
			elif [[ $port = "139" ]] || [[ $port = "445" ]]; then
				enum_smb_service $host $port
			fi
			printf "${YELLOW}===============================================================\n${NC}"
		done
	}

	if [ $# -eq 0 ] || [ $1 = "-h" ] || [ $1 = "--help" ]; then
		echo "Usage: $0 <HOST>"
		exit
	else
		host=$1
	fi

	enum_all_port $host

	printf "${GREEN}[+] $ports\n${NC}"

	enum_open_service $host $ports

	array_port=$(echo $ports | tr ',' '\n')

	recon $array_port
	```