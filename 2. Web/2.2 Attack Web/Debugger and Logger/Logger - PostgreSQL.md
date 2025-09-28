---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/debugger-and-logger/logger-postgre-sql/","noteIcon":"","created":"2025-04-15T14:11:19.600-04:00"}
---




















### PostgreSQL

1. **Edit the PostgreSQL configuration file**:
```bash
    sudo nano /etc/postgresql/{version}/main/postgresql.conf
```
Windows system
```powershell
    C:\Program Files
(x86)\ManageEngine\AppManager12\working\pgsql\data\amdb\postgresql.conf
```
   
2. **Add or modify the following settings**:
    ```ini
    log_statement = 'all'
    logging_collector = on
    log_directory = 'pg_log'
    log_filename = 'postgresql-%Y-%m-%d.log'
    ```

3. **Restart PostgreSQL**:
```bash
    sudo systemctl restart postgresql
```

Restart the service. 
```
services.msc

```

4. **view logs**
```
C:\Program Files (x86)\ManageEngine\AppManager12\working\pgsql\data\amdb\pgsql_log\
swissql*
```


# login
```
sudo -u postgres psql postgres
```