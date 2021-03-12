# Information Gathering

## whois

``` bash
whois leecybersec.com
```

## nslookup

``` bash
nslookup leecybersec.com
```

## Google Hacking

``` bash
site:leecybersec.com filetype:html
```

``` bash
site:leecybersec.com -filetype:html
```

``` bash
intitle:"index of" "backup"
```

[Google Hacking Database](https://www.exploit-db.com/google-hacking-database)

## [Netcraft](https://www.netcraft.com/)

Netcraft’s DNS search: [https://searchdns.netcraft.com](https://searchdns.netcraft.com)

``` bash
https://searchdns.netcraft.com/?restriction=site+contains&host=.leecybersec.com&position=limited
```

"site report": [https://sitereport.netcraft.com](https://sitereport.netcraft.com)

``` bash
https://sitereport.netcraft.com/?url=https%3A%2F%2Fleecybersec.com
```

## Recon-ng

``` bash
marketplace search site
```

``` bash
marketplace info recon/domains-hosts/bing_domain_web
```

``` bash
marketplace install recon/domains-hosts/bing_domain_web
```

``` bash
modules load recon/domains-hosts/bing_domain_web
```

``` bash
options set source leecybersec.com
```

## Open-source github
158
## Shodan