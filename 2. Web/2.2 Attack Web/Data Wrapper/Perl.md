---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/data-wrapper/perl/","noteIcon":"","created":"2025-04-15T14:11:19.598-04:00"}
---

















### **5. Perl**

|**Wrapper/Technique**|**Description**|**Example Exploit**|
|---|---|---|
|**`eval()`**|Executes arbitrary Perl code.|`eval("system('whoami')");`|
|**`open()` with pipes**|Executes shell commands via open function.|`open(FH, "|
|**`qx// (backticks)`**|Executes commands inline.|`$output = qx(whoami); print $output;`|

---