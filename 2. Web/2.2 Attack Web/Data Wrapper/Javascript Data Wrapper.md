---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/data-wrapper/javascript-data-wrapper/","noteIcon":"","created":"2025-04-15T14:11:19.598-04:00"}
---


















### **4. JavaScript (Node.js)**

|**Wrapper/Technique**|**Description**|**Example Exploit**|
|---|---|---|
|**`eval()`**|Executes arbitrary JavaScript code.|`eval("console.log('Injected Code')")`|
|**`Function()`**|Creates dynamic JavaScript functions.|`let f = new Function("return process"); f().mainModule.require('child_process').exec('whoami');`|
|**`child_process.exec()`**|Executes shell commands in Node.js.|`require('child_process').exec('whoami', console.log);`|

---

