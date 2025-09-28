
### ✅ macOS Architecture Summary:

| Layer          | Description                                                             |
| -------------- | ----------------------------------------------------------------------- |
| **Darwin**     | The core OS layer, open-source, based on **BSD Unix** + **Mach kernel** |
| **XNU Kernel** | Hybrid kernel combining **Mach (microkernel)** and **BSD (monolithic)** |


---

## 📦 macOS Kernel Stack

### Kernel Base: **XNU**

- Originally stands for **X is Not Unix**
    
- Hybrid design: Mach (message passing, memory) + BSD (processes, sockets)
    
- Used in: macOS, iOS, iPadOS, watchOS, tvOS
    

---

## 📐 macOS Memory Layout (x86_64)

While the kernel is different, **virtual memory** on macOS behaves similarly to Linux **at the user space level**, because both conform to **POSIX**. But details differ.

### Example Layout (64-bit macOS)

```text
0x0000000100000000 ─────── main executable (.text/.data/.bss)
0x0000000100100000 ─────── heap (malloc)
0x00007ffee0000000 ─────── stack top (grows down)
0x00007fff20300000 ─────── shared cache (dyld, libc, etc.)
```

### Shared regions:

- macOS uses a **"shared cache"** for system libraries like `libSystem.dylib`, `libc.dylib`, etc.
    
- This is similar to `libc.so` on Linux but managed differently and placed in **high memory**.
    

---

## 🔐 ASLR & Protections in macOS

|Protection|Supported on macOS?|Notes|
|---|---|---|
|**ASLR**|Yes|Full 64-bit ASLR (stack, heap, libs, PIE binaries)|
|**DEP (NX)**|Yes|Non-executable memory supported|
|**SIP (System Integrity Protection)**|Yes|Blocks modifying system memory, even as root|
|**Stack canaries**|Yes|Enabled by default|

