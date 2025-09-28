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

