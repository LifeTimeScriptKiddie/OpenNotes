---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/debugger-and-logger/logger-sq-lite/","noteIcon":"","created":"2025-04-15T14:11:19.601-04:00"}
---

















### SQLite

For SQLite, logging is typically handled within the application code due to its embedded nature. Here is an example using Python:

```python
import sqlite3

# Connect to SQLite database
conn = sqlite3.connect('example.db')

# Enable query logging
def log_query(query):
    with open('sqlite_queries.log', 'a') as f:
        f.write(query + '\n')

# Example of logging a query
query = "SELECT * FROM users"
log_query(query)
conn.execute(query)
```

