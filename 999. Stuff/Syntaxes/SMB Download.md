---
dg-publish: true
---
```
sudo apt update && sudo apt install cifs-utils -y
sudo mkdir -p /mnt/windows_share

# Try modern NTLMSSP with SMB3
sudo mount.cifs //<IP>/ShareDrive /mnt/windows_share \
  -o username=<username>,password=<password>,vers=3.0,sec=ntlmssp,uid=$(id -u),gid=$(id -g)

# If that errors, fallback:
dmesg | tail -20

# Then try SMB2.1
sudo umount /mnt/windows_share
sudo mount.cifs //<IP>/ShareDrive /mnt/windows_share \
  -o username=<Username>,password=<password>,vers=2.1,sec=ntlmssp,uid=$(id -u),gid=$(id -g)

```