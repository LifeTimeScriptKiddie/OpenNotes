

```text
0x00000000 ─────────────────────────────────────── NULL page
              Unmapped — access here causes segmentation fault

0x00001000 ─────────────────────────────────────── Start of mapped memory
              .text segment (code), .data (globals), .bss (zero-inited)

0x08048000 ─────────────────────────────────────── Default base address of ELF binaries (non-PIE)
               Entry point of your main program (main executable)

0x10000000 ─────────────────────────────────────── Heap
               malloc(), new, dynamic memory allocation
               Grows upward as you allocate more

0x40000000 ─────────────────────────────────────── mmap() region
               Shared libraries like libc, libm, libpthread, etc.
               This is randomized by ASLR (like your 0x77fxxxxx libc region)

0x77f00000 ──────┐
                 │
               libc.so region (~1 MB window)
                 Executable + readable (r-xp), randomized by ASLR
0x77fff000 ──────┘

0xbfff0000 ─────────────────────────────────────── Stack bottom
               Stack starts here (or slightly lower)

0xbfffffff ─────────────────────────────────────── Stack top
               Stack grows **downward** toward lower addresses

────────────────────────────────────────────────── 3 GB = max user space

0xc0000000 ─────────────────────────────────────── Kernel space (not accessible from user mode)
               Protected memory — system calls, drivers, kernel code
               User-to-kernel transition via syscalls

0xffffffff ─────────────────────────────────────── End of 4 GB address space
```

---

##  Visual Diagram Summary

```text
Virtual Address Range (32-bit userland layout)
──────────────────────────────────────────────
|    Address    | Region             | Notes                        |
|---------------|--------------------|------------------------------|
| 0x00000000    | NULL               | Segfault if accessed         |
| 0x08048000    | Binary .text/.data | Program code, globals        |
| 0x10000000    | Heap               | malloc(), grows upward       |
| 0x40000000    | mmap region        | Shared libs (libc, etc.)     |
| 0x77f00000    | libc.so (ASLR)     | Executable gadgets for ROP   |
| 0xbfff0000    | Stack              | Grows downward               |
| 0xc0000000    | Kernel space       | Not accessible from userland |
```

---

##  ASLR Zones (Entropic Regions)

|Memory Region|Typical ASLR Entropy|Guess Count|Exploitability|
|---|---|---|---|
|Stack|8 bits (≈256 pages)|Easy|Stack overflow w/ ROP possible|
|Heap|8–12 bits|Easy-Med|Can leak/use heap pointers|
|mmap (libc)|8 bits (1 MB window)|Easy|🔥 Common for ret2libc & gadgets|
|Binary (PIE)|0 (non-PIE) or 8–16|Medium|Must compile with PIE|

---

Would you like to compare this with **64-bit layout** or simulate a `cat /proc/self/maps` to see it in real memory?