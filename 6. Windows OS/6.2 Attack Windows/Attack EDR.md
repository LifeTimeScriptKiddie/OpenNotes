
```mermaid
graph TD
    A[Attacker Entry Point] --> B{Attack Vectors}

    B --> C[Fileless Malware]
    C --> C1[Uses PowerShell, WMI, Macros]
    C1 --> C2[Resides in Memory]
    C2 --> C3[Evades File-Based Detection]
    C1 --> C4[Bypasses AMSI using Reflection or Patching]

    B --> D[Living Off the Land Binaries]
    D --> D1[rundll32 exe]
    D --> D2[regsvr32 exe]
    D --> D3[mshta exe]
    D1 --> D4[Executes Malicious Code]
    D2 --> D4
    D3 --> D4

    B --> E[PowerShell Bypasses]
    E --> E1[Bypass AMSI via Reflection]
    E --> E2[Patch AmsiScanBuffer]
    E --> E3[Set amsiInitFailed]
    E --> E4[Load Fake amsi dll]
    E1 --> E5[Evade Script Blocking]
    E2 --> E5
    E3 --> E5
    E4 --> E5

    B --> F[Exploits and Vulnerabilities]
    F --> F1[Unpatched OS or App]
    F1 --> F2[Remote Code Execution or Priv Esc]

    B --> G[Credential Theft]
    G --> G1[Dump LSASS with Mimikatz]
    G --> G2[Extract Plaintext or Hashes]
    G2 --> G3[Lateral Movement or Persistence]

    B --> H[Persistence Mechanisms]
    H --> H1[Scheduled Tasks]
    H --> H2[Registry Run Keys]
    H --> H3[WMI Event Subscription]
    H --> H4[DLL Hijacking]

    B --> I[Malicious Drivers and Rootkits]
    I --> I1[Kernel-Level Access]
    I1 --> I2[Stealthy Code Execution]

    B --> J[Phishing and Social Engineering]
    J --> J1[Emails with Malicious Attachments]
    J --> J2[Fake Login Pages]
    J --> J3[Links to Exploit Kits]

```

1. **Fileless Malware**: This type of malware resides in memory and doesn't write files to disk, making it harder for traditional antivirus solutions to detect. It often uses legitimate system tools like PowerShell, WMI, or macros to execute malicious code directly in memory.
    
2. **Living Off the Land Binaries (LOLBins)**: Attackers can abuse legitimate system tools and binaries that are already present on Windows, like `rundll32.exe`, `regsvr32.exe`, or `mshta.exe`, to run malicious payloads, blending in with normal operations and avoiding detection.
    
3. **Exploits and Vulnerabilities**: Attackers often exploit unpatched vulnerabilities in the operating system, drivers, or applications to gain unauthorized access or escalate privileges.
    
4. **Credential Theft**: Tools like Mimikatz can extract credentials from memory, allowing attackers to move laterally across a network or escalate their privileges.
    
5. **Persistence Mechanisms**: Attackers use various techniques to maintain persistence on a compromised system, such as registry modifications, scheduled tasks, WMI persistence, or DLL hijacking.
    
6. **Malicious Drivers and Rootkits**: By installing malicious drivers or rootkits, attackers can operate at the kernel level, making their presence harder to detect and remove.
    
7. **Phishing and Social Engineering**: Attackers frequently use phishing emails, malicious attachments, or compromised websites to trick users into running malicious code or divulging credentials.
    