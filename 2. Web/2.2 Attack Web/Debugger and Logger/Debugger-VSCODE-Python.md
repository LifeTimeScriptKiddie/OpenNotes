---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/debugger-and-logger/debugger-vscode-python/","noteIcon":"","created":"2025-04-15T14:11:19.600-04:00"}
---


















// Use IntelliSense to learn about possible attributes.
// Hover to view descriptions of existing attributes.
// For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
```
"version": "0.2.0",
"configurations": [
  {
    "name": "Python: Remote Attach",
    "type": "python",
    "request": "attach",
    "port": 5678,
    "host": "<Your_ERPNext_IP>",
    "pathMappings": [
      {
      "localRoot": "${workspaceFolder}",
      "remoteRoot": "/home/frappe/frappe-bench/"
      }
    ]
  }
  ]
}
```
