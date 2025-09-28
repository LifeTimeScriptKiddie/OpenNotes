### Remote Debugging with Docker and Node.js
1. **Update `docker-compose.yml` to enable debugging:**
   ```yaml
   version: '3.7'
   services:
     chips:
       build: .
       command: node --inspect=0.0.0.0:9229 server.js
   ```

2. **Start the application with debugging enabled:**
   ```bash
   student@oswe:~/chips$ docker-compose up
   ```

3. **Configure `launch.json` for Node.js debugging in Visual Studio Code:**
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
           }
       ]
   }
   ```

4. **Start the debugging session in Visual Studio Code:**
   - Open the debug panel and select the configuration.
   - Set breakpoints and step through the code as needed   .