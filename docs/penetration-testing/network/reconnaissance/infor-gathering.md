# Information Gathering

## [OSINT Framework](https://osintframework.com)

## [Maltego](https://www.maltego.com)

## Searching Domain

whois

``` bash
whois leecybersec.com
```

nslookup

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

## Theharvester

``` bash
theHarvester -d leecybersec.com -b google
```

## [linkedin2username](https://github.com/initstring/linkedin2username)

``` bash
python3 linkedin2username.py -u 'linkedin-username' -n <domain> -c <company-name>
```

## Source Code

[About searching on GitHub](https://docs.github.com/en/github/searching-for-information-on-github/about-searching-on-github)

``` bash
in:file web user:leecybersec
```

``` bash
gitleaks -v -r=https://github.com/leecybersec/client-splunk
```

## [Shodan](https://shodan.io)

[Searching Shodan For Fun And Profit](https://www.exploit-db.com/docs/english/33859-searching-shodan-for-fun-and-profit.pdf)


* `city`: find devices in a particular city
* `country`: find devices in a particular country
* `geo`: you can pass it coordinates
* `hostname`: find values that match the hostname
* `net`: search based on an IP or /x CIDR
* `os`: search based on operating system
* `port`: find particular ports that are open
* `before/after`: find results within a timeframe

## [Security Header](https://securityheaders.com)

``` bash
https://securityheaders.com/?q=leecybersec.com&followRedirects=on
```

## [SSL Labs](https://www.ssllabs.com)

``` bash
https://www.ssllabs.com/ssltest/analyze.html?d=leecybersec.com&latest
```

## [Social Searcher](https://www.social-searcher.com)

``` bash
https://www.social-searcher.com/social-buzz/?q5=leecybersec.com
```