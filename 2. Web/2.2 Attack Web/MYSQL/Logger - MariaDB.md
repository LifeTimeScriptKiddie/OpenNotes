---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/mysql/logger-maria-db/","noteIcon":"","created":"2025-04-15T14:11:19.607-04:00"}
---

















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

