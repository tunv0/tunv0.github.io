# Basic Services

## Running services

Checking running services

``` bash
sudo ss -antlp
```

Checking all available services

``` bash
systemctl list-unit-files
```

## SSH Service

``` bash
sudo systemctl start ssh
```

SSH service start automatically at boot time.

``` bash
sudo systemctl enable ssh
```

## Web Service

Apache2

``` bash
sudo systemctl start apache2
```

Python

``` bash
python3 -m http.server 80

python -m SimpleHTTPServer 80
```

php

``` bash
php -S 0.0.0.0:80
```
busybox

``` bash
busybox httpd -f -p 80
```

HTTP service start automatically at boot time.

``` bash
sudo systemctl enable apache2
```