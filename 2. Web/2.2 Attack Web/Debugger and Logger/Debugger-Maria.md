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
