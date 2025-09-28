
# 1. Stealthy Port Scanning Techniques

## 1.1 Nmap with Stealth Options

- **SYN scan (half-open)**:
    
    ```
    nmap -sS -Pn -T2 --max-rate=50 --open <target>
    ```
    
    - `-sS`: SYN scan (doesn’t complete TCP handshake)
        
    - `-Pn`: Skip host discovery
        
    - `--max-rate=50`: Throttle packet rate
        
    - `--open`: Only show open ports
        

## 1.2 Fragmentation

- Splits packets to evade signature detection:
    
    ```
    nmap -f -sS -Pn <target>
    ```
    

## 1.3 Decoy Scanning

- Obfuscate source IP by mixing with decoys:
    
    ```
    nmap -sS -D RND:10 <target>
    ```
    
    - Random decoy IPs make attribution harder.
        

## 1.4 Idle/Zombie Scan

- Spoofs third-party host as source (requires predictable IPID):
    
    ```
    nmap -sI <zombie_ip> <target>
    ```
    

## 1.5 Timing & Rate Limiting

- Use slow timings to reduce detection:
    
    ```
    nmap -sS -T1 <target>
    ```
    

---

# 2. Stealthy IP Discovery Techniques

## 2.1 Passive Recon (No Packet Sent)

- **NetFlow logs**, DNS records, WHOIS, Shodan, etc.
    
- **OSINT tools**: Amass, Maltego, etc.
    

## 2.2 DNS Zone Transfer (if misconfigured)

```
dig axfr @ns.target.com target.com
```

## 2.3 ARP Scanning (on internal subnets)

- Tools: `arp-scan`, `netdiscover`
    
    ```
    arp-scan -I eth0 --localnet
    ```
    

## 2.4 Slow ICMP Echo Scan (if allowed)

```
fping -a -g <ip-range>
```

---

# 3. From Compromised Hosts (Internal Recon)

Once inside:

- Use **Netstat** to find active connections:
    
    ```
    netstat -ano
    ```
    
- Use **PowerShell** or `WMIC`:
    
    ```powershell
    Get-NetTCPConnection
    wmic process list full
    ```
    
- **SharpHound** and **BloodHound**: For internal asset discovery stealthily.
    

---

# 4. Using Cobalt Strike

- Use **portscan** alias or custom script:
    
    ```powershell
    beacon> powershell -nop -w hidden -c "1..65535 | % { try { (New-Object Net.Sockets.TcpClient).Connect('10.0.0.5', $_); \"Port $_ open\" } catch {} }"
    ```
    
- Spread scans across multiple beacons to avoid traffic spikes.
    