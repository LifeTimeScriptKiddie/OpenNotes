

## **✅ BLUF:**

  

You _can_ extract firmware from the ESP32 using external hardware like a **SPI flash reader** or by **connecting directly to the chip’s SPI flash pins**, but it’s often easier and safer to use the UART method unless the flash chip is locked or damaged.

---

## **🧰 1.** **Easiest Method — UART via USB (What You’re Already Doing)**

  

This is using esptool.py over the built-in USB-to-serial converter (or UART pins).

```
esptool.py --chip esp32 --port /dev/cu.usbserial-120 read_flash 0x000000 0x400000 esp32_firmware.bin
```

> ✅ Recommended unless the chip or bootloader is disabled/protected.

---

## **🧰 2.** **Hardware-Based Method — SPI Flash Dump via External Reader**

  

### **Use this when:**

- The ESP32 is damaged or bricked
    
- UART access is disabled (e.g., for anti-tamper reasons)
    
- You want to clone an unpowered device
    

  

### **✅ What You Need:**

- **External SPI flash reader/writer**, like:
    
    - **CH341A programmer**
        
    - **Bus Pirate**
        
    - **FTDI SPI module**
        
    
- **SOIC8 test clip** if the flash chip is soldered down
    
- Flash memory dump software (e.g., flashrom)
    

  

### **🧷 Physical Pinout (typical W25Q32 flash chip):**

|**Pin**|**Function**|**Notes**|
|---|---|---|
|1|/CS|Chip select|
|2|DO (MISO)|Data out|
|3|WP#|Write protect (tie high)|
|4|GND|Ground|
|5|DI (MOSI)|Data in|
|6|CLK|Clock|
|7|HOLD#|Tie high|
|8|VCC|3.3V ONLY (⚠️ 5V = 🔥)|

> ⚠️ Always confirm with a multimeter and datasheet before wiring.

---

## **🔥 Example Using**  flashrom with CH341A**

```
flashrom -p ch341a_spi -r esp32_dump.bin
```

> You may need to run as root (sudo) and disable system SIP protections on macOS.

---

## **🧠 Security Note**

  

Most ESP32s **do not encrypt flash by default**, but if **flash encryption** is enabled, the dumped binary will be **useless** without the encryption key stored in eFuses.

---

## **🧪 Summary**

|**Method**|**Tool Required**|**Difficulty**|**Best For**|
|---|---|---|---|
|UART (esptool.py)|None (USB cable)|🟢 Easy|Normal firmware reading|
|SPI Flash Dump|CH341A, clip, etc.|🔴 Advanced|Bricked chips or UART locked|
|JTAG|JTAG debugger|🔴 Hard|Live debugging, rare for reading full firmware|
