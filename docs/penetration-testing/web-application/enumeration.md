# Enumeration

## Enum follow

- Inspecting URLs
- Inspecting Page Content
- Viewing Response Headers
- Inspecting Sitemaps
- Locating Administration Consoles

## Recon web

1. Check cookies
2. Check "admin" and "Admin", "admin " and "admin"
3. Check the redirection

Authentication

1. Check IDOR
2. Check .js, .json
3. Check Object-relational mapping (&admin[admin]=1)

## List all URLs

``` bash
curl http://$ip -s -L | grep "title\|href" | sed -e 's/^[[:space:]]*//'
```

## Web Discovery

gobuster

``` bash
gobuster dir -u http://$ip/cgi-bin/ -w /usr/share/seclists/Discovery/Web-Content/ -x txt,sh,php,cgi -s '200,204,403,500'
```

``` bash
gobuster dir -u http://$ip/ -w /usr/share/seclists/Discovery/Web-Content/cgis.txt
```

dirb

``` bash
dirb http://$1:$2/ /usr/share/wordlists/dirb/common.txt -r
```

## Nikto

``` bash
nikto -h $ip
```