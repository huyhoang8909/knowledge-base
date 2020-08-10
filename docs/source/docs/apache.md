# Apache

## Get installed modules

### V2.2
apachectl -t -D DUMP_MODULES

## Apache 2.4
### Enable rewrite log

```
LogLevel alert rewrite:trace6
tail -f error_log|fgrep '[rewrite:'
```

### Restart apache
sudo apachectl -t
sudo apachectl graceful
