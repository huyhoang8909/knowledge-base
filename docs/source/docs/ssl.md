# SSL
## subfolder ssl
wp-config.php

```
if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] == 'https') { 
 
    define('WP_HOME', 'https://example.com/abc/');
    define('WP_SITEURL', 'https://example.com/abc/');
 
    // http://wordpress.org/support/topic/compatibility-with-wordpress-behind-a-reverse-proxy
    $_SERVER['HTTPS'] = 'on';
}
```

config https

```

<VirtualHost *:443>
        ServerName example.com
        ServerAdmin info@example.com
        DocumentRoot /usr2/symfony/example.com/web
        ErrorLog  "|/usr/sbin/rotatelogs /usr2/log/apache2/example.com/ssl_error_log.%Y%m%d 86400 540"
        CustomLog "|/usr/sbin/rotatelogs /usr2/log/apache2/example.com/ssl_access_log.%Y%m%d 86400 540" combined
        <Directory "/usr2/symfony/example.com/web">
                Options FollowSymLinks
                AllowOverride All
                Order deny,allow
                Allow from all
        </Directory>

        #Use for http://example.com/abc
        RequestHeader set X_FORWARDED_PROTO https
        ProxyPass /abc/ http://160.16.209.248:8080/abc/
        ProxyPassReverse /abc/ http://160.16.209.248:8080/abc/

        # Use for secondsite.com
        ProxyPreserveHost On
        RedirectMatch 301 ^/secondsite/(.*)$ http://secondsite.com/$1

        Alias /sf /usr/lib/php/data/symfony/web/sf

        <Directory "/usr/lib/php/data/symfony/web/sf">
                AllowOverride All
                Allow from all
        </Directory>

        <Location />
                ErrorDocument 403 http://example.com/
                Order allow,deny
                Allow from all
        </Location>
</VirtualHost>
```
redirect

```
 RewriteEngine on
 RewriteCond %{REQUEST_URI} /abc/?.*$
 RewriteRule .* https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

