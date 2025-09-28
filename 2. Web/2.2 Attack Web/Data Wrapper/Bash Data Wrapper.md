### **1. Bash (Process Substitution & Here Documents)**

|**Technique**|**Description**|**Example Exploit**|
|---|---|---|
|**Process Substitution**|Reads command output as a file stream.|`cat <(echo "Injected Code")`|
|**Here Documents**|Injects multi-line data into commands.|`cat << EOF > payload.sh; echo "whoami"; EOF; bash payload.sh`|
|**File Descriptor Wrapping**|Accesses file descriptors directly.|`cat /proc/self/fd/0 <<< "Injected Data"`|

---
