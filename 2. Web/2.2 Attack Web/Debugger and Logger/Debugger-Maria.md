---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/debugger-and-logger/debugger-maria/","noteIcon":"","created":"2025-04-15T14:11:19.600-04:00"}
---



















```
/etc/mysql/my.cnf
sudo nano /etc/mysql/my.cnf
[mysqld]
...
general_log_file = /var/log/mysql/mysql.log
general_log = 1


sudo vim /etc/mysql/my.cnf

sudo systemctl restart mysql

sudo tail -f /var/log/mysql/mysql.log
```
