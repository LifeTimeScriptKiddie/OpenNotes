### **4. JavaScript (Node.js)**

|**Wrapper/Technique**|**Description**|**Example Exploit**|
|---|---|---|
|**`eval()`**|Executes arbitrary JavaScript code.|`eval("console.log('Injected Code')")`|
|**`Function()`**|Creates dynamic JavaScript functions.|`let f = new Function("return process"); f().mainModule.require('child_process').exec('whoami');`|
|**`child_process.exec()`**|Executes shell commands in Node.js.|`require('child_process').exec('whoami', console.log);`|

---

