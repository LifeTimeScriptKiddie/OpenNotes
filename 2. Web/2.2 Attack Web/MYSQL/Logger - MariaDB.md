# MariaDB Query Logging


```bash
   frappe@ubuntu:~$ sudo nano /etc/mysql/my.cnf
```

```ini
   [mysqld]
   general_log_file        = /var/log/mysql/mysql.log
   general_log             = 1
```

```bash
   frappe@ubuntu:~$ sudo systemctl restart mysql
   frappe@ubuntu:~$ sudo tail -f /var/log/mysql/mysql.log
```

