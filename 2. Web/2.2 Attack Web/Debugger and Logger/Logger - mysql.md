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
