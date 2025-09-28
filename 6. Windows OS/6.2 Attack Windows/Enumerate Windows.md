---
{"dg-publish":true,"permalink":"/attack-computer/attack-windows/enumerate-windows/","noteIcon":"","created":"2025-04-15T14:11:19.623-04:00"}
---




















## Windows Enumeration Techniques


| **Category**               | **Technique**                          | **Description**                                                                          | **Tools/Commands**                                   |
| -------------------------- | -------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| **System Information**     | Gather System Info                     | Collect basic system details such as OS version, architecture, and installed patches.    | systeminfo<br><br>wmic os get osarchitecture         |
|                            | List Installed Updates                 | Identify installed patches and updates for vulnerability assessment.                     | wmic qfe get<br><br>Get-Hotfix                       |
| **Environment Variables**  | Enumerate Environment Variables        | Check for sensitive data stored in environment variables.                                | set<br>Get-ChildItem Env:                            |
| **User Information**       | List Users and Groups                  | Identify local users and group memberships.                                              | net users<br><br>net localgroup, <br><br>whoami /all |
|                            | Check Password Policies                | Review password policies for potential weaknesses.                                       | net accounts                                         |
| **Processes and Services** | List Running Processes                 | Identify running processes for potential insights.                                       | tasklist<br>Get-Process                              |
|                            | Check Service Permissions              | Find services with misconfigured permissions.                                            | `sc qc`, `accesschk.exe`                             |
| **Network Configuration**  | View Network Interfaces                | Get information on network interfaces and configurations.                                | `ipconfig /all`, `Get-NetIPConfiguration`            |
|                            | List Open Ports                        | Identify open ports and listening services.                                              | `netstat -ano`                                       |
|                            | Check Firewall Rules                   | Review firewall settings and rules.                                                      | `netsh advfirewall show allprofiles`                 |
| **Scheduled Tasks**        | Enumerate Scheduled Tasks              | Identify tasks that may run with elevated privileges.                                    | `schtasks /query`, `Get-ScheduledTask`               |
| **Registry Enumeration**   | Search for Sensitive Registry Entries  | Look for registry keys that may contain credentials or configuration data.               | `reg query`                                          |
| **File System**            | Find Interesting Files and Directories | Search for files containing sensitive information like passwords or configuration files. | `dir /s *pass*`, `Get-ChildItem`                     |
|                            | Check File and Folder Permissions      | Identify files or folders with weak permissions.                                         | `icacls`, `accesschk.exe`                            |
| **Credentials**            | Check Credential Manager               | Look for saved credentials in the Windows Credential Manager.                            | `cmdkey /list`                                       |
|                            | Examine Browser Credentials            | Review saved passwords and autofill data in browsers.                                    | Use browser-specific tools                           |
| **Logging and Auditing**   | Review Event Logs                      | Analyze event logs for anomalies or important information.                               | `eventvwr.msc`, `Get-EventLog`                       |
| **Network Shares**         | Enumerate Network Shares               | Identify accessible network shares.                                                      | `net view`, `net use`                                |
| **Installed Applications** | List Installed Software                | Identify installed applications for potential vulnerabilities or management.             | `wmic product get`, `Get-WmiObject`                  |

---

## Mermaid Diagram of Windows Enumeration Techniques
```mermaid
graph LR

A[User, Privilege, Group]
B[Computer info]
C[Network info]

A --> A1[net users, net localgroup, whoami /all, net user username, Get-LocalUser]
A1 --> A11[net accounts]


B --> B1[OS]
B1 --> B11[systeminfo,  wmic os get osarchitecture]
B1 --> B12[wmic qfe get,  Get-Hotfix]

B --> B2[Process and Services]
B2 --> B21[tasklist, Get-Process]
B21 --> B211[Permission check: sc qc, accesschk.exe]


B --> B3[Registry]
B3 --> B31[reg query]

B --> B4[Scheduled Tasks]
B4 --> B41[schtasks /query, Get-ScheduledTask]

B --> B5[Environment]
B5--> B51[set,  Get-ChildItem Env:]

B --> B6[Interesting Files/software]
B6 --> B61[File/Folder Permission : icacls, accesschk.exe]
B6 --> B62[wmic product get, Get-WmiObject]

B7[Credentials]--> B71[cmdkey /list]
B7 --> B72[findstr /si password *.txt *.ini *.config]

B --> B8[Logging/Auditing]
B8 --> B81[eventvwr.msc, Get-EventLog]


C--> C1[Network]
C1 --> C11[ipconfig /all, Get-NetIPConfiguration]
C1 --> C12[Firewall: netsh advfirewall show allprofiles]
C1 --> C13[route print, arp -a]


C--> C2[Network share]
C2 --> C21[net view, net use]

```

---
