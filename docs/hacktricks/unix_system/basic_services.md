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

## HTTP Service

Apache2

``` bash
sudo systemctl start apache2
```

Python3

``` bash
python3 -m http.server 8080

python -m SimpleHTTPServer 8888
```

php

``` bash
php -S 192.168.11.130:8000
```

HTTP service start automatically at boot time.

``` bash
sudo systemctl enable apache2
```