### Oracle Database

1. **Edit the Oracle initialization parameter file**:
    ```sql
    ALTER SYSTEM SET log_checkpoints_to_alert = TRUE;
    ALTER SYSTEM SET log_archive_trace = 1;
    ALTER SYSTEM SET audit_trail = DB,EXTENDED SCOPE=SPFILE;
    ```

2. **Restart the Oracle Database**:
    ```sql
    SHUTDOWN IMMEDIATE;
    STARTUP;
    ```

