---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/debugger-and-logger/logger-mysql/","noteIcon":"","created":"2025-04-15T14:11:19.601-04:00"}
---

















```
/etc/mysql/my.cnf
sudo vim /etc/mysql/my.cnf


check 
/var/lib/mysql

# Update
general_log_file = /var/log/mysql/mysql.log
general_log = 1
```
Restart the server
sudo systemctl restart mysql

Monitor log
```
sudo tail –f /var/log/mysql/mysql.log
```
