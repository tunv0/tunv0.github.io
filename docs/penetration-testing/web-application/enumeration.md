# Enumeration

## Check version, platform

## List all URLs

``` bash
curl http://$ip -s -L | grep "title\|href" | sed -e 's/^[[:space:]]*//'
```

## Discovery files and directories

``` bash
gobuster dir -u http://$ip/cgi-bin/ -w /usr/share/seclists/Discovery/Web-Content/ -x txt,sh,php,cgi -s '200,204,403,500'
```

``` bash
gobuster dir -u http://$ip/ -w /usr/share/seclists/Discovery/Web-Content/cgis.txt
```

## Nikto

``` bash
nikto -h $ip
```