# General

## Reference

[Common Ports and Services](https://oscp.infosecsanyam.in/untitled/common-ports-and-services)

[0daysecurity Enumeration](http://www.0daysecurity.com/penetration-testing/enumeration.html)

## Service unknown - Port XXX
``` bash
$ amap -d $ip $port
amap v5.4 (www.thc.org/thc-amap) started at 2020-09-09 23:30:39 - APPLICATION MAPPING mode

Protocol on <ip>:<port>/tcp matches ftp
Dump of identified response from <ip>:<port>/tcp (by trigger http):
0000:  3232 3020 4d69 6372 6f73 6f66 7420 4654    [ 220 Microsoft FT ]
0010:  5020 5365 7276 6963 650d 0a35 3030 2043    [ P Service..500 C ]
0020:  6f6d 6d61 6e64 206e 6f74 2075 6e64 6572    [ ommand not under ]
0030:  7374 6f6f 642e 0d0a 3530 3020 436f 6d6d    [ stood...500 Comm ]
0040:  616e 6420 6e6f 7420 756e 6465 7273 746f    [ and not understo ]
0050:  6f64 2e0d 0a                               [ od...            ]
```