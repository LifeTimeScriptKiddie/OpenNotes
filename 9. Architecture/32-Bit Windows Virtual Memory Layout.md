

## Notes and Exploitation Insights

| Region                  | Use Case / Exploit Relevance                    |
| ----------------------- | ----------------------------------------------- |
| `0x00000000`            | Null pointer dereference (legacy usermode bugs) |
| `0x00100000`            | Entry point of main executable                  |
| `0x60000000–0x70000000` | ROP gadgets in system DLLs                      |
| `0x70000000–0x7FFE0000` | `ntdll.dll`, crucial for syscall-based exploits |
| `0x7FFE0000–0x7FFEFFFF` | KUSER_SHARED_DATA used in information leaks     |
| `0x7FFF0000–0x7FFFFFFF` | Stack buffer overflows                          |
|                         |                                                 |




```
0x00000000 ────────────── NULL page
              Reserved. Accessing this address causes an access violation (exception).

0x00010000 ────────────── Start of usable user space
              First valid allocation page. This is where heap or DLLs may start.

0x00100000 ────────────── Typical base address of PE executables
              The .text, .data, .rdata, .bss sections of the main EXE are loaded here.

0x10000000 ────────────── Common base for non-ASLR DLLs
              Application-specific or statically linked DLLs may appear here.

0x20000000 – 0x40000000 ─ Dynamically reserved/committed memory
              Heap allocations via `HeapAlloc` or `VirtualAlloc` often show up here.

0x40000000 – 0x60000000 ─ Memory-mapped files, shared memory
              Memory created via `CreateFileMapping`, `MapViewOfFile`, or IPC usage.

0x60000000 – 0x70000000 ─ Shared libraries
              System DLLs (e.g., `user32.dll`, `gdi32.dll`, `advapi32.dll`) loaded with or without ASLR.

0x70000000 – 0x7FFE0000 ─ Core system module region
              `ntdll.dll` is typically mapped here. Critical for syscall stubs and ROP chains.

0x7FFE0000 – 0x7FFEFFFF ─ KUSER_SHARED_DATA
              Read-only memory shared between kernel and user space. Contains system time, tick count, etc.

0x7FFF0000 – 0x7FFFFFFF ─ Stack top
              The thread stack grows downward from this region. Stack overflows target this region.

────────────────────────────────────────────────────────────

0x80000000 – 0xFFFFFFFF ─ Kernel space
              Reserved for the Windows kernel and drivers. Inaccessible from user-mode processes.
```

---
