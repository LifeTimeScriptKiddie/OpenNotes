---
{"dg-publish":true,"permalink":"/learn-programming/learn-rust/rust-cross-compilation-guide-linux-to-windows/","noteIcon":"","created":"2025-04-15T14:11:19.625-04:00"}
---


















## 1. Install Rust Windows Target in Ubuntu (WSL/Linux)
To compile Rust programs on **Ubuntu (or WSL) for Windows**, install the **Windows target**:
```bash
rustup target add x86_64-pc-windows-gnu
```

## 2. Install MinGW for Cross Compilation
To generate Windows `.exe` files from Linux, install MinGW:
```bash
sudo apt update
sudo apt install mingw-w64 -y
```

## 3. Create a New Rust Project (Optional)
If you don’t already have a Rust project:
```bash
cargo new my_project
cd my_project
```

## 4. Modify Cargo.toml (Optional)
If your project uses Windows APIs, add the `windows` crate:
```toml
[dependencies]
windows = { version = "0.52", features = ["Win32_System_Memory", "Win32_System_Threading", "Win32_Foundation"] }
```

## 5. Compile for Windows
To **compile a Rust project for Windows** from Ubuntu:
```bash
cargo build --release --target x86_64-pc-windows-gnu
```
The Windows `.exe` file will be in:
```
target/x86_64-pc-windows-gnu/release/my_project.exe
```

## 6. Move the EXE to Windows
To copy the EXE to your Windows environment **(if using WSL)**:
```bash
cp target/x86_64-pc-windows-gnu/release/my_project.exe /mnt/c/Users/YourUsername/Desktop/
```
Now you can execute it from Windows:
```powershell
C:\Users\YourUsername\Desktop\my_project.exe
```

## 7. Running the EXE on Windows
From **Windows CMD or PowerShell**:
```powershell
cd C:\Users\YourUsername\Desktop
.\my_project.exe
```

---

## Summary
| **Step** | **Command** |
|----------|------------|
| Install Rust Windows Target | `rustup target add x86_64-pc-windows-gnu` |
| Install MinGW | `sudo apt install mingw-w64 -y` |
| Compile Rust for Windows | `cargo build --release --target x86_64-pc-windows-gnu` |
| Copy EXE to Windows | `cp target/x86_64-pc-windows-gnu/release/my_project.exe /mnt/c/Users/YourUsername/Desktop/` |
| Run EXE on Windows | `C:\Users\YourUsername\Desktop\my_project.exe` |

