---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/debugger-and-logger/debugger-java-vscode/","noteIcon":"","created":"2025-04-15T14:11:19.599-04:00"}
---



















### Remote Debugging with Visual Studio Code (Java Application)
1. **Install Visual Studio Code and required extensions:**
   ```bash
   kali@kali:~$ sudo apt install ~/Downloads/code_1.45.1-1589445302_amd64.deb
   ```

2. **Set up `launch.json` for remote debugging:**
   ```json
   {
       "version": "0.2.0",
       "configurations": [
           {
               "type": "java",
               "request": "attach",
               "name": "Attach to Remote Program",
               "hostName": "127.0.0.1",
               "port": 8888
           }
       ]
   }
   ```
2a. **another Setup**

```json
{
"version": "0.2.0",
"configurations": [
{
"type": "node",
"request": "attach",
"name": "Attach to remote",
"address": "chips",
"port": 9229,
"localRoot": "${workspaceFolder}",
"remoteRoot": "/usr/src/app"
},
{
"type": "node",
"request": "attach",
"name": "Attach to remote (cli)",
"address": "chips",
"port": 9228,
"localRoot": "${workspaceFolder}",
"remoteRoot": "/usr/src/app"
}
]
}
```

   

3. **Start the Java application with remote debugging:**
   ```bash
   kali@kali:~$ java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=9898 -jar NumberGame.jar
   ```

4. **Attach the debugger in Visual Studio Code:**
   - Open `MainController.java` and set a breakpoint.
   - Start debugging by selecting the configuration from the debug panel.

5. **Verify the debugger connection and step through the code:**
   - Submit a request on the web page to trigger the breakpoint.
   - Use the debugging context menu to step over, into, or out of code, and continue execution as needed   .
