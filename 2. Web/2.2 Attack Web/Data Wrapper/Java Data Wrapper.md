### **3. Java (Runtime, ProcessBuilder, Java Reflection)**

|**Wrapper/Technique**|**Description**|**Example Exploit**|
|---|---|---|
|**Runtime.exec()**|Executes shell commands.|`Runtime.getRuntime().exec("whoami")`|
|**ProcessBuilder**|Builds system command execution.|`new ProcessBuilder("cmd.exe", "/c", "dir").start();`|
|**Java Reflection**|Dynamically calls methods at runtime.|`Class.forName("java.lang.Runtime").getMethod("exec", String.class).invoke(null, "whoami");`|

---
