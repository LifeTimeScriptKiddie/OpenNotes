---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/data-wrapper/java-data-wrapper/","noteIcon":"","created":"2025-04-15T14:11:19.598-04:00"}
---


















### **3. Java (Runtime, ProcessBuilder, Java Reflection)**

|**Wrapper/Technique**|**Description**|**Example Exploit**|
|---|---|---|
|**Runtime.exec()**|Executes shell commands.|`Runtime.getRuntime().exec("whoami")`|
|**ProcessBuilder**|Builds system command execution.|`new ProcessBuilder("cmd.exe", "/c", "dir").start();`|
|**Java Reflection**|Dynamically calls methods at runtime.|`Class.forName("java.lang.Runtime").getMethod("exec", String.class).invoke(null, "whoami");`|

---
