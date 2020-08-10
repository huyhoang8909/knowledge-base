# Centos

## Add user to group
sudo usermod -aG groupName userName

## Create new user
adduser username
passwd username

### Test
su - username

## Sudo configuration
/usr/sbin/visudo
chmod 700 .ssh

## SSH config
sudo vi /etc/ssh/sshd_config

### Reload
service sshd reload

## List all groups of a user
groups userName



## Backup server

rsync --rsh="ssh server@abc sudo" -avz --exclude=/proc --exclude=/sys --exclude=/dev --exclude '*.log' --exclude '*.gz' / ~/VPSBackup/abc

sudo tar -zcvpf backup/fbackup-mysql-data`date -I`.tar.gz --directory / --exclude=mnt --exclude=proc --exclude=tmp  --exclude=sys --exclude=dev --exclude '*.log' --exclude=var/log --exclude=var/www --exclude=var/lib/mysql --exclude=home --exclude 'var/cache/nginx/cache' .



## Search log
grep "04/Oct/2017:01" /var/log/nginx/abc.access.log | grep -c -v "wp-includes\|wp-admin\|wp-content"
grep "04/Oct/2017:01" /var/log/nginx/abc.access.log | grep "HIT" -c

## Search latest modified
find . -name '*.php' -type f -exec ls -lt {} + | grep -v .git | less

## Search word
grep -rlw "yahoo" .

## Find command
```
find -type d -name 2017-* -exec rmdir {} \;
find /www/backup/ -maxdepth 1 -type df -mtime +100 -exec rm -rf "{}" \;
```

## Search and replace
find /www/api -type f -exec sed -i 's/abc\.co/abc\.co\.vn/g' {} \;

## Httpd passs
http://www.luft.co.jp/cgi/htpasswd.php
htpasswd -b /www/sites/example.com/.htpasswd test test

## Update datetime
https://www.cyberciti.biz/faq/howto-set-date-time-from-linux-command-prompt/

```
sudo ln -sf /usr/share/zoneinfo/Asia/Ho_Chi_Minh /etc/localtime
export TZ=Asia/Ho_Chi_Minh
date
date +%T%p -s "6:10:30AM"
```

## Sync folder

unison -batch /var/www/html/abc/wp-content/uploads/ ssh://wp01///var/www/html/abc/wp-content/uploads/


## Qmail
https://www.experts-exchange.com/questions/23186361/Web-based-Qmail-statistics.html
https://www.dotdeb.org/2008/10/13/calculate-statistics-from-your-qmail-logfiles-using-awstats/

## Convert encoding mac
iconv -f sjis -t utf-8 < file > file.new

## Redis

***backup redis
A$ redis-cli
127.0.0.1:6379> SAVE
scp /var/lib/redis/dump.rdb web-04:/tmp/dump.rdb
sudo service redis stop
sudo cp /tmp/dump.rdb /var/lib/redis/dump.rdb
sudo chown redis: /var/lib/redis/dump.rdb
sudo service redis start

## Repos
https://centos.pkgs.org/5/utter-ramblings-x86_64/

## Update php-xml for centos 5

sudo yum remove php php-cli php-common
sudo yum remove mysql mysql-devel mysql-server
wget http://vault.centos.org/5.11/os/x86_64/CentOS/libxslt-1.1.17-4.el5_8.3.x86_64.rpm
sudo yum install libxslt-1.1.17-4.el5_8.3.x86_64.rpm 
sudo yum --disablerepo=base,remi*,epel,atomic install  php php-cli php-common php-devel php-mbstring php-pdo php-mysql php-xml
sudo yum --disablerepo=base,remi*,epel,atomic install mysqlclient15
wget http://vault.centos.org/5.11/os/x86_64/CentOS/perl-DBD-MySQL-3.0007-2.el5.x86_64.rpm
sudo rpm -i perl-DBD-MySQL-3.0007-2.el5.x86_64.rpm
sudo yum install --disablerepo=base,remi*,epel,atomic mysql mysql-devel mysql-server
sudo mv /etc/my.cnf /etc/my.cnf.bk
sudo mv /etc/my.cnf.rpmsave /etc/my.cnf
wget http://vault.centos.org/5.11/updates/x86_64/RPMS/dovecot-1.0.7-9.el5_11.4.x86_64.rpm
sudo rpm -i dovecot-1.0.7-9.el5_11.4.x86_64.rpm
wget http://vault.centos.org/5.11/os/x86_64/CentOS/postfix-2.3.3-7.el5.x86_64.rpm
sudo rpm -i postfix-2.3.3-7.el5.x86_64.rpm
sudo mv /etc/postfix/main.cf /etc/postfix/main.cf.bk
sudo mv /etc/postfix/main.cf.rpmsave /etc/postfix/main.cf
sudo mv /etc/postfix/canonical /etc/postfix/canonical.bk
sudo mv /etc/postfix/canonical.rpmsave /etc/postfix/canonical
sudo mv /etc/dovecot.conf /etc/dovecot.conf.bk
sudo mv /etc/dovecot.conf.rpmsave /etc/dovecot.conf
sudo service postfix restart
sudo service dovecot restart
sudo mv /etc/php.ini /etc/php.ini.bk
sudo mv /etc/php.ini.rpmsave /etc/php.ini
sudo service httpd restart



