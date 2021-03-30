# VulnHub WinterMute: 1 (Straylight)

> Author: Hades - [LeeCyberSec](https://leecybersec.com)

> [*Scripting here*](https://github.com/leecybersec/scripting)

## VM Details

|**Name**|WinterMute: 1|
|---|---|
|**Date release**|5 Jul 2018|
|**Author**|[creosote](https://www.vulnhub.com/author/creosote,584/)|
|**Series**|[WinterMute](https://www.vulnhub.com/series/wintermute,161/)|

## Information Gathering

### Openning Services

After get root at [WinterMute: 1 (Straylight)](/walkthrough/vulnhub/Wintermute-1-Straylight/)
I enum the network and saw that there are 2 interfaces `enp0s3` and `enp0s8`.

``` txt
root@straylight:/tmp# ifconfig
enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.56.102  netmask 255.255.255.0  broadcast 192.168.56.255
        inet6 fe80::a00:27ff:fe0e:1b0d  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:0e:1b:0d  txqueuelen 1000  (Ethernet)
        RX packets 498352  bytes 66009694 (62.9 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 408318  bytes 173600084 (165.5 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

enp0s8: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.107.106  netmask 255.255.255.0  broadcast 192.168.107.255
        inet6 fe80::a00:27ff:fec0:db47  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:c0:db:47  txqueuelen 1000  (Ethernet)
        RX packets 244  bytes 34210 (33.4 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 45  bytes 7450 (7.2 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
<snip>
```

> [*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/vulnhub/wintermute-1-straylight)

``` txt
root@straylight:/tmp# bash pingSweeping.sh 192.168.107
192.168.107.2
192.168.107.1
192.168.107.106
192.168.107.107
```

Scan open port in `192.168.107.107` with `nc`.

``` bash
root@straylight:/tmp# nc -nv -w 1 -z 192.168.107.107 1-65535
(UNKNOWN) [192.168.107.107] 34483 (?) open
(UNKNOWN) [192.168.107.107] 8080 (http-alt) open
(UNKNOWN) [192.168.107.107] 8009 (?) open
```