### Microsoft SQL Server

1. **Open SQL Server Management Studio** and connect to your database.

2. **Create a new server-side trace**:
    ```sql
    DECLARE @TraceID INT;
    EXEC sp_trace_create @TraceID OUTPUT, 2, N'C:\Path\To\Your\LogFile.trc', 5, NULL;
    EXEC sp_trace_setevent @TraceID, 10, 1, 1;
    EXEC sp_trace_setevent @TraceID, 10, 2, 1;
    EXEC sp_trace_setevent @TraceID, 10, 3, 1;
    EXEC sp_trace_setevent @TraceID, 10, 4, 1;
    EXEC sp_trace_setevent @TraceID, 10, 12, 1;
    EXEC sp_trace_setstatus @TraceID, 1;
    ```

3. **Stop and delete the trace when done**:
    ```sql
    EXEC sp_trace_setstatus @TraceID, 0;
    EXEC sp_trace_setstatus @TraceID, 2;
    ```

