### **5. Perl**

|**Wrapper/Technique**|**Description**|**Example Exploit**|
|---|---|---|
|**`eval()`**|Executes arbitrary Perl code.|`eval("system('whoami')");`|
|**`open()` with pipes**|Executes shell commands via open function.|`open(FH, "|
|**`qx// (backticks)`**|Executes commands inline.|`$output = qx(whoami); print $output;`|

---