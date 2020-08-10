# Debug php

## 1 . Laravel
### Functions
```
dd()
dump()
var_dump()
```

Ref more: https://laravel.com/docs/5.8/helpers

### laravel log file

#### Location
```
    storage/logs
```
#### Configuration
```
.env
```
with the following content

```
APP_DEBUG=true
APP_LOG_LEVEL=debug
```

### Debug in console

```
php -a
php artisan tinker
```

## 2. Pysh
```
eval(\Psy\sh());
```
https://psysh.org/
https://www.sitepoint.com/interactive-php-debugging-psysh/

## 3. Xdebug, profiler
https://packagecontrol.io/packages/Xdebug%20Client
https://kipalog.com/posts/Debug-voi-Xdebug-va-Sublime-Text

## 4. DB debug
### Enale query log
https://tecadmin.net/enable-logs-in-mysql/

### Debug for a certain query in Laravel

```

DB::enableQueryLog(); // Enable query log

// Your Eloquent query

dd(DB::getQueryLog()); // Show results of log
```
