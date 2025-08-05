# 🚨 ESP32 Wi-Fi Penetration Tool

A universal and lightweight Wi-Fi penetration testing toolkit built for the ESP32 platform. This project enables various Wi-Fi attack techniques like PMKID capture, handshake capture, and rogue AP deployment, all from a small, cheap, low-power SoC.

> ⚠️ **Disclaimer**: This project is for educational and authorized security testing purposes **only**. Do not use this tool against networks you do not own or have explicit permission to test.

---

## 📦 Features

* 📡 Wi-Fi handshake and PMKID capture
* 🚫 Deauthentication attack
* 🎭 Rogue access point duplication
* 💻 Simple web interface for attack configuration
* 💾 PCAP file export for offline cracking

> ❌ **Note:** Hash cracking is **not** performed on the ESP32 due to hardware limitations. Use external tools like `aircrack-ng` on a more powerful system (e.g., Kali Linux).

---

## 🧰 Prerequisites

* ESP32 development board
* [esptool](https://github.com/espressif/esptool) installed
* `bootloader.bin`, `partition-table.bin`, `esp32-wifi-penetration-tool.bin` binaries
* A system with Wi-Fi (to connect to ESP32's AP)
* Kali Linux with `aircrack-ng` for hash cracking

---

## 🚀 Flashing the ESP32

Use the following command to flash the firmware:

```bash
esptool.exe --port COM6 -b 115200 --after hard_reset write_flash --flash_mode dio --flash_freq 40m --flash_size detect 0x8000 partition-table.bin 0x1000 bootloader.bin 0x10000 esp32-wifi-penetration-tool.bin
```

<img width="1380" height="660" alt="Screenshot 2025-08-05 215631" src="https://github.com/user-attachments/assets/7f248bc3-809a-4cd0-b993-7f1cb55770c9" />

Replace `COM6` with the correct port on your system.

---

## 🌐 Web Interface

1. After flashing, ESP32 will create an AP (e.g., `ESP32_PenTest`).
2. Connect your computer to this Wi-Fi.
3. Open your browser and go to:

   ```
   http://192.168.4.1
   ```

<img width="631" height="551" alt="Screenshot 2025-08-05 214202" src="https://github.com/user-attachments/assets/ad3bc2f8-39a0-4e1a-9af3-0f069a160a76" />

---

## ⚙️ Launching an Attack

1. **Select Wi-Fi SSID** of the target network.
2. Set:

   * **Attack Type**: `ATTACK_TYPE_HANDSHAKE`
   * **Attack Method**: `DEAUTH_ROGUE_AP (PASSIVE)`
3. Click **Start Attack**.
4. Traffic will be captured and saved as a `.pcap` file.

<img width="610" height="747" alt="Screenshot 2025-08-05 220840" src="https://github.com/user-attachments/assets/13e218b5-b8b6-4f32-8350-91aa53ccc2fa" />


---

## 🔓 Cracking the Password

Once you have the `capture.pcap`, move it to your Kali Linux system.

### Step 1: Basic cracking

```bash
aircrack-ng capture.pcap -w rockyou.txt
```
<img width="633" height="433" alt="Screenshot 2025-08-05 214022" src="https://github.com/user-attachments/assets/7aff33fb-839f-48d7-b15f-ca68fa16ed48" />


### Step 2: Target a specific network

1. From the previous command output, note the **BSSID** of the target.
2. Run:

```bash
aircrack-ng capture.pcap -w rockyou.txt -e kali -b <bssid>
```

<img width="627" height="70" alt="Screenshot 2025-08-05 214058" src="https://github.com/user-attachments/assets/102f5dbc-e8ce-4543-9228-26db109a3ee7" />
<img width="647" height="380" alt="Screenshot 2025-08-05 214044" src="https://github.com/user-attachments/assets/3803d2c6-bd52-41b2-898f-4bbc07e9daf3" />


Replace `<bssid>` with the captured one.

If the password exists in the `rockyou.txt` wordlist, it will be cracked and displayed.



Would you like me to also generate a `project structure` or `bin file download guide` section for your README?
