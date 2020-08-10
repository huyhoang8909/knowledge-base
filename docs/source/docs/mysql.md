# Mysql
## Dump db and ignore the certain tables
mysqldump -uroot -h127.0.0.1 mydb --ignore-table=mydb.abc --ignore-table=mydb.de | gzip > ~/backup/`date +"%Y-%m-%d_%H"`_mini_mydb.sql.gz
