# Enumeration

## Enum follow

- Inspecting URLs
- Inspecting Page Content
- Viewing Response Headers
- Inspecting Sitemaps `robots.txt`, `sitemap.xml`
- Locating Administration Consoles

``` bash
curl http://$ip
```

``` bash
curl http://$ip -s -L | grep "title\|href" | sed -e 's/^[[:space:]]*//'
```

## Recon web

1. Check cookies
2. Check the redirection
3. Check SQLi `admin' or '1'='1`
4. Check credentials `admin` and `Admin`, `admin ` and `admin`

Authentication

1. Check IDOR
2. Check .js, .json
3. Check Object-relational mapping (&admin[admin]=1)

## Virtual hosting

> Virtual hosting is a method for hosting multiple domain names (with separate handling of each name) on a single server (or pool of servers).

``` bash
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://$host -H 'Host: FUZZ.$domain' -fw number
```

``` bash
gobuster vhost -u erev0s.com -w awesome_wordlist.txt
```

Reference: [https://erev0s.com/blog/gobuster-directory-dns-and-virtual-hosts-bruteforcing](https://erev0s.com/blog/gobuster-directory-dns-and-virtual-hosts-bruteforcing)

## Web Discovery

ffuf

``` bash
ffuf -s -w /usr/share/seclists/Discovery/Web-Content/common.txt -u "$url:$port/FUZZ" -e $ext -fw number
```

gobuster

``` bash
gobuster dir -u http://$ip/cgi-bin/ -w /usr/share/seclists/Discovery/Web-Content/ -x txt,sh,php,cgi -s '200,204,403,500'
```

dirb

``` bash
dirb http://$ip:$port/ /usr/share/wordlists/dirb/common.txt -r
```

## Nikto

``` bash
nikto -h $ip
```