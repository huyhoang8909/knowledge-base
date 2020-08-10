# Build PHP from source

sudo tar xf php-5.6.40.tar.gz
cd php-5.6.40
sudo ./configure --prefix=/usr/share/php56 --with-openssl --enable-mbstring --with-mcrypt --with-mhash --with-mysql --with-mysqli --with-openssl --with-pcre-regex --with-pdo-mysql --with-zlib-dir --with-regex --enable-sysvsem --enable-sysvshm --enable-sysvmsg --enable-soap --enable-sockets --with-xmlrpc --enable-zip --with-zlib --enable-inline-optimization --enable-mbregex --without-pear
sudo make && sudo make install
sudo cp php.ini-production /usr/share/php56/lib/php.ini

## reate file /www/example/cgi-bin/php-cgi
```
#!/bin/sh
#PHPRC=/etc/php55
#export PHPRC
export PHP_FCGI_MAX_REQUESTS=5000
export PHP_FCGI_CHILDREN=8
exec /usr/share/php56/bin/php-cgi
```

## Virtual hosts

```
    <Directory "/www/example/http/example.com/public">
        Options -Indexes FollowSymLinks +ExecCGI
        AllowOverride All
        AddHandler php5-fastcgi .php
        Action php5-fastcgi /cgi-bin/php-cgi
        Order allow,deny
        Allow from all
    </Directory>

    <Directory "/www/example/cgi-bin">
        AllowOverride None
        Options None
        Order allow,deny
        Allow from all
    </Directory>
```
