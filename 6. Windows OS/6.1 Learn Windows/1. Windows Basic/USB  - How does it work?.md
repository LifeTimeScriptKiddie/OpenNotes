---
{"dg-publish":true,"permalink":"/attack-computer/attack-windows/1-windows-basic/usb-how-does-it-work/","noteIcon":"","created":"2025-04-15T14:11:19.617-04:00"}
---



















```mermaid
graph TD
    A[USB Device Plugged In] --> B[Power Supplied]
    B --> C[Plug and Play Manager Detects USB Device]
    C --> D[USB Stack Initialized]
    D --> E[Device Enumeration]
    E --> F{Driver Found in Driver Store?}
    F -->|Yes| G[Load Driver from Driver Store]
    F -->|No| H[Search Windows Update for Driver]
    H --> I[Download and Install Driver]
    G --> J{Is Device a Storage Device?}
    J -->|Yes| K[Mount Manager Assigns Drive Letter]
    J -->|No| L[Device Ready for Use]
    K --> L
    L --> M[File Explorer Displays Device]

```


| Component/Service           | Role                                                                 | File/Service Name            |
| --------------------------- | -------------------------------------------------------------------- | ---------------------------- |
| USB Device Plugged In       | User connects the USB device to the computer.                        | N/A                          |
| Power Supplied              | Laptop provides power to the USB device for initialization.          | N/A                          |
| Plug and Play (PnP) Manager | Detects new hardware and initiates the process to recognize the USB. | `umpnpmgr.dll`, `pnpmgr.sys` |
| USB Stack                   | Manages communication between the OS and USB device drivers.         | `usbhub.sys`, `usbstor.sys`  |
| Driver Store                | Stores pre-installed drivers for various hardware devices.           | N/A                          |
| Windows Update              | Searches online for drivers if not found locally.                    | `wuaueng.dll`                |
| Mount Manager               | Mounts storage devices, assigning a drive letter.                    | `mountmgr.sys`               |
| Device Manager              | Provides an interface for viewing and managing connected devices.    | `devmgmt.msc`                |
| File Explorer               | Allows the user to interact with the device (e.g., browsing files).  | `explorer.exe`               |
