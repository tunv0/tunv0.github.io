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
sudo ssh -N -L 0.0.0.0:80:10.10.10.10:8080 hades@192.168.11.133 -i ./.ssh/id_rsa
```

### Remote Forwarding

``` bash
ssh -N -R [bind_address:]port:host:hostport [username@address]
```

``` bash
ssh -N -R 0.0.0.0:9001:10.10.10.10:80 kali@myip -i /home/hades/.ssh/kalali-idrsa
```

### Dynamic Forwarding

## Plink.exe

## NetSH

## HTTPTunnel-ing