---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/debugger-and-logger/debugger-erp-next-frappe/","noteIcon":"","created":"2025-04-15T14:11:19.599-04:00"}
---



















1. **SMTP Server Setup**:
==why?== 
To send emails to bypass the password reset functionality. 

```bash
kali@kali:~$ ssh frappe@192.168.121.123
frappe@ubuntu:~$ sudo nano /home/frappe/frappe-bench/sites/site1.local/site_config.json
```
```json
{
"db_name": "_1bd3e0294da19198",
"db_password": "32ldabYvxQanK4jj",
"db_type": "mariadb",
"mail_server": "192.168.45.219",
"use_ssl": 0,
"mail_port": 25,
"auto_email_id": "admin@randomdomain.com"
}
```
   ```bash
   kali@kali:~$
   sudo python3 -m smtpd -n -c DebuggingServer 0.0.0.0:25 
   ```

2. **Remote Debugging Setup**:
Download vscode. Install ptvsd, and comment out web server, to start the server later. 
   ```bash
   kali@kali:~$ sudo apt install ~/Downloads/code_1.45.1-1589445302_amd64.deb
   frappe@ubuntu:~$ /home/frappe/frappe-bench/env/bin/pip install ptvsd
   frappe@ubuntu:~$ sudo vim /home/frappe/frappe-bench/Procfile
   ```
   ```bash
   # Comment out the web server line
   #web: bench serve --port 8000
   ```


==Python ptvsd to set up debugger. ==

```python
   # /home/frappe/frappe-bench/apps/frappe/frappe/app.py
import ptvsd
ptvsd.enable_attach(redirect_output=True)
print("Now ready for the IDE to connect to the debugger")
ptvsd.wait_for_attach()

````
```bash
kali@kali:~$ rsync -azP frappe@192.168.121.123:/home/frappe/frappe-bench ./
```

3. **MariaDB Query Logging**:
```bash
frappe@ubuntu:~$ sudo vim /etc/mysql/my.cnf
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

### 5.2 Start the frappe server
```
cd /home/frappe/frappe-bench/

bench start


cd /home/frappe/frappe-bench/sites

../env/bin/python ../apps/frappe/frappe/utils/bench_helper.py frappe serve --port 8000 --noreload --nothreading

```

