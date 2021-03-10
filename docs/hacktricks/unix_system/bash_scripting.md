# Bash Scripting

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

## Arguments and If Else

=== "Running"

	``` bash
	chmod +x .sh

	./.sh
	```

=== "hello_world.sh"

	``` bash

	```

`108`