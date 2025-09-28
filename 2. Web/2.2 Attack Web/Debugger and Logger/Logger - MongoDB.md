---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/debugger-and-logger/logger-mongo-db/","noteIcon":"","created":"2025-04-15T14:11:19.600-04:00"}
---




















### MongoDB

1. **Edit the MongoDB configuration file**:
    ```bash
    sudo nano /etc/mongod.conf
    ```
   
2. **Add or modify the following settings**:
    ```yaml
    systemLog:
      destination: file
      path: /var/log/mongodb/mongod.log
      logAppend: true
    operationProfiling:
      mode: all
    ```

3. **Restart MongoDB**:
    ```bash
    sudo systemctl restart mongod
    ```
