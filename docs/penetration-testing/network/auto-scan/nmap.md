# nmap

## All Port Scan

### TCP

``` bash
nmap -p- -T3 $ip -o all_tcp.nmap
```

### UDP

``` bash
sudo nmap -sU -p- $ip -o all_udp.nmap
```

### ports

``` bash
ports=$(cat all_tcp.nmap | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//); echo $ports
```

###

``` bash

```

###

``` bash

```

###

``` bash

```