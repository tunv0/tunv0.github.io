# smtp 25

## <a href='https://www.ionos.com/digitalguide/e-mail/technical-matters/smtp/' target="blank">What is SMTP? Definition and basics</a>

## Server Connection

``` bash
$ nc -nvC $ip 25
$ telnet $ip 25

EXPN
VRFY <user>
```

## Scanning Vul

``` bash
$ nmap $ip -p 25 --script=smtp-*

$ sudo msfconsole -q -x "setg RHOSTS $ip;
use auxiliary/scanner/smtp/smtp_enum; run;
use auxiliary/scanner/smtp/smtp_relay; run;
use auxiliary/scanner/smtp/smtp_version; run;
exit"
```

## SMTP Common Commands

``` bash
$ helo admin
$ mail from:<>
$ rcpt to:<nobody>
$ data
hades
.
```