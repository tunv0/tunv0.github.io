# Terminal

## Bash Environment

``` bash
echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

### Set an environment variable

``` bash
export ip=192.168.11.131
```

``` bash
ping $ip
nmap $ip
```

### All environment variables

``` bash
env
```

### Edit .zshrc

``` bash
alias cpu="grep 'cpu ' /proc/stat | awk '{usage=(\$2+\$4)*100/(\$2+\$4+\$5)} END {print usage}' | awk '{printf(\"%.1f\n\", \$1)}'"
alias ram="free | grep Mem | awk '{print \$3/\$2 * 100.0}' | awk '{printf(\"%.1f\n\", \$1)}'"
alias myip='ip add | grep "inet " | grep -v "127.0.0.1" | cut -d"/" -f1 | cut -d " " -f 6 | tail -1'
```

``` bash
PROMPT=$'%F{%(#.blue.green)}┌──${debian_chroot:+($debian_chroot)──}(%B%F{%(#.red.blue)}Hades%(#.💀.㉿)%b$(myip)%F{%(#.blue.green)})-[$(cpu):$(ram)]%B%F{reset}%(6~.%-1~/…/%4~.%5~)%b%F{%(#.blue.green)}\n└─%B%(#.%F{red}#.%F{blue}$)%b%F{reset} '
```

## Background commands

=== "Background a process"

	``` bash
	nmap -p- 127.0.0.1 &
	```

=== "Suspend the job"

	``` bash
	┌──(Hades㉿192.168.11.130)-[0.7:11.1]~
	└─$ nmap -p- 192.168.11.131 -Pn

	Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
	Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-09 20:52 EST
	^Z
	zsh: suspended  nmap -p- 192.168.11.131 -Pn
	┌──(Hades㉿192.168.11.130)-[0.7:11.4]~
	└─$ bg

	[1]  + continued  nmap -p- 192.168.11.131 -Pn
	```

=== "jobs and fg"

	``` bash
	┌──(Hades㉿192.168.11.130)-[0.7:11.1]~
	└─$ jobs

	[1]  + running    nmap -p- 192.168.11.131 -Pn
	                                                                                                                                                                            
	┌──(Hades㉿192.168.11.130)-[0.8:11.4]~
	└─$ fg

	[1]  + running    nmap -p- 192.168.11.131 -Pn
	^C
	```

## History

### Re-run the first command

``` bash
!1
```

### Repeats the last command

``` bash
!!
```

## Exit code

Exit code 0 denotes a program’s successful execution.

Non-zero exit code denotes an unsuccessful execution of a program

``` bash
echo $?
```

## Bash Scripting

[https://devhints.io/bash](https://devhints.io/bash)

[https://github.com/leecybersec/scripting](https://github.com/leecybersec/scripting)

### Hello World

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

### My Self Script

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

### Arguments and If Else

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

### Loops and Functions

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

### Auto Enum Script

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

	if [ -z $1 ]; then
		echo "Usage: $0 <HOST>"
		exit
	else
		host=$1
		ports=$2
		service=$3
	fi

	enum_all_port ()
	{
		printf "\n${YELLOW}Scanning openning port ...\n${NC}"
		if [ -z $ports ]; then
			ports=$(nmap -sS -p- --min-rate 1000 $host | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//)
		fi

		if [ -z $ports ]; then
			printf "${RED}[-] Found no openning port!${NC}"
			exit
		else
			printf "${GREEN}[+] Openning ports: $ports\n${NC}"
			array_ports=$(echo $ports | tr ',' '\n')
		fi
	}

	enum_open_service ()
	{
		printf "\n${YELLOW}===============================services===============================\n${NC}"

		echo "nmap -sC -sV -Pn $1 -p$2"
		nmap -sC -sV $host -p$ports
	}

	enum_smtp_service ()
	{
		printf "\n${YELLOW}===============================$port===============================\n${NC}"

		echo "nmap $host -p$port -Pn --script=smtp-*"
		nmap $host -p$port --script=smtp-*
	}

	enum_web_service ()
	{
		printf "\n${YELLOW}===============================$url===============================\n${NC}"

		printf "\n${GREEN}[+] Files and directories\n${NC}"
		echo "gobuster dir -k -u $url:$port -w /usr/share/seclists/Discovery/Web-Content/common.txt"
		gobuster dir -k -u $url:$port -w /usr/share/seclists/Discovery/Web-Content/common.txt

		printf "\n${GREEN}[+] All URLs\n${NC}"
		curl -k $url:$port -s -L | grep "title\|href" | sed -e 's/^[[:space:]]*//'
	}

	enum_smb_service ()
	{
		printf "\n${YELLOW}===============================$port===============================\n${NC}"

		echo "smbmap -H $host"
		smbmap -H $host

		echo "smbclient -L $host"
		smbclient -NL $host
	}

	recon ()
	{
		if [ -z $service ]; then
			
			for port in $array_ports; do
				if [ $port = "25" ]; then

					enum_smtp_service $host $port

				elif [ $port = "80" ]; then

					url="http://$host"
					enum_web_service $url $port

				elif [ $port = "443" ]; then

					url="https://$host"
					enum_web_service $url $port

				elif [ $port = "445" ]; then

					enum_smb_service $host $port

				fi
			done

		else

			port=$ports		

			if [ $service = "smtp" ]; then

				enum_smtp_service $host $port

			elif [ $service = "http" ]; then

				url="http://$host"
				enum_web_service $url $port

			elif [ $service = "https" ]; then

				url="https://$host"
				enum_web_service $url $port

			elif [ $service = "smb" ]; then

				enum_smb_service $host $port

			fi

		fi
	}

	main ()
	{
		enum_all_port $host $ports
		
		enum_open_service $host $ports

		recon $array_ports $service
	}

	main
	```