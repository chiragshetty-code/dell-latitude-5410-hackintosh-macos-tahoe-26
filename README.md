# Dell Latitude 5410 — macOS Tahoe 26 Hackintosh

**OpenCore EFI for Dell Latitude 5410 (i5-10310U, UHD 620, 16GB RAM)**

A fully functional macOS Tahoe 26 (Intel) installation on a Dell Latitude 5410, built from scratch, debugged extensively, and documented for the community.

---

## 📌 Overview

This repository contains a working OpenCore EFI configuration for running **macOS 26 "Tahoe"** on a **Dell Latitude 5410** laptop.

It covers the complete journey, including:
- The initial macOS installation
- Post-install fixes for audio, backlight, SD card, and Wi-Fi
- Solving the notorious post-update black screen issue
- Using OpenCore Legacy Patcher (OCLP-Mod) correctly

Built by a 17-year-old who broke his screen, lost his partition, survived a 40GB iCloud cache bomb, and kept going.

---

## 💻 Hardware Specifications

| Component | Model |
| :--- | :--- |
| **Laptop** | Dell Latitude 5410 |
| **CPU** | Intel Core i5-10310U (Comet Lake, 10th Gen) |
| **GPU** | Intel UHD Graphics 620 (identified as UHD 630 in macOS) |
| **RAM** | 16GB DDR4 |
| **Storage** | NVMe SSD |
| **Audio** | Realtek ALC3204 (Intel SST) |
| **Wi-Fi/BT** | Intel AX201 |
| **Display** | 1366×768 (originally 1080p) |
| **Bootloader** | OpenCore 1.0.0+ |

---

## ✅ What Works

| Feature | Status |
| :--- | :--- |
| macOS 26 Tahoe | ✅ Fully functional |
| Intel UHD 620 Graphics | ✅ Full acceleration |
| Wi-Fi (itlwm + HeliPort) | ✅ Working |
| Ethernet | ✅ Working |
| Bluetooth | ✅ Working |
| **Audio (Speakers + Mic)** | ✅ **Working (via OCLP-Mod root patch)** |
| **Backlight Control** | ✅ **Working (requires specific boot-args)** |
| **SD Card Reader** | ✅ **Working (via RealtekCardReader.kext)** |
| USB Ports | ✅ Working |
| Apple ID / iCloud / App Store | ✅ Working |
| FaceTime | ✅ Working |
| Dual-boot with Windows 11 | ✅ Working |
| Sleep / Wake | ✅ Working |
| Battery Management | ✅ Working |

---

## ❌ What Doesn't Work

| Feature | Status | Workaround |
| :--- | :--- | :--- |
| iMessage | ❌ WIP | Requires fix for Intel Wi-Fi link quality issue. FaceTime works. |
| HDMI | ❌ Untested | Needs LSPCON framebuffer patching. |
| Built-in Microphone | ✅ Working | Fixed via OCLP-Mod audio patch. |

---

## 🛠️ Tools Used

- **OpenCore** — Bootloader
- **OCAT (OpenCore Auxiliary Tools)** — Config editor
- **USBToolBox** — USB mapping
- **GenSMBIOS** — Serial generator
- **itlwm + HeliPort** — Wi-Fi
- **HoRNDIS** — USB tethering
- **OCLP-Mod** — Root patching for audio and Wi-Fi
- **Hackintool** — Debugging and info
- **DiskGenius** — EFI editing from Windows

---

## 🔧 Critical Fixes

### 1. Audio Fix (Post-Update)

**Problem:** macOS 26.7 and later remove AppleHDA.kext, causing total loss of audio (speakers and mic) after any OS update.

**Solution:** Use **OCLP-Mod** to apply the Modern Audio patch.

**Steps:**
1. Install the correct **Kernel Debug Kit (KDK)** for your exact macOS build (e.g., `KDK_26.7_25G229.kdk`).
2. Place the KDK in `/Library/Developer/KDKs/`.
3. Run OCLP-Mod → **Post Install Root Patch** → **Start Root Patching**.
4. Reboot.

**Note:** This fix requires the KDK to be manually installed. OCLP's automatic KDK retrieval is currently broken for macOS 26.7.

### 2. Backlight Fix (The Real Culprit)

**Problem:** After updating to macOS 26.7, the backlight would not turn on during a **cold boot**. The screen was on, but the backlight was off (visible only with a flashlight). Warm reboots worked, cold boots did not.

**Root Cause:** The EFI was missing a critical boot-argument for Comet Lake backlight control. macOS 26.6.2 tolerated its absence, but 26.7 did not.

**Solution:** Add `-igfxblr` to your boot-args.

**Steps:**
1. Open your `config.plist` in **OCAT**.
2. Go to **NVRAM → Add → `7C436110-AB2A-4BBB-A880-FE41995C9F82`**.
3. Edit the **`boot-args`** value to include:-v debug=0x100 keepsyms=1 -amfipassbeta -igfxblr -igfxblt -vi2c-force-polling
4. Save and reboot.

**Why it works:** `-igfxblr` fixes the backlight register initialization for Coffee Lake and Comet Lake platforms, ensuring the display backlight activates on a cold boot.

### 3. SD Card Reader Fix

**Problem:** The built-in Realtek RTS525A SD card reader is not natively supported by macOS.

**Solution:** Use the `RealtekCardReader.kext` and `RealtekCardReaderFriend.kext`.

**Steps:**
1. Download the latest `RealtekCardReader.kext` from the [0xFireWolf/RealtekCardReader](https://github.com/0xFireWolf/RealtekCardReader) repository.
2. Place it in `EFI/OC/Kexts/`.
3. Add it to your `config.plist` under **Kernel → Add**.
4. Optionally, install `RealtekCardReaderFriend.kext` to make macOS recognize it as a built-in device.
5. Reboot and reset NVRAM.

### 4. Wi-Fi Fix

**Problem:** The Intel AX201 Wi-Fi card is not natively supported by macOS.

**Solution:** Use `itlwm.kext` alongside the **HeliPort** app.

**Steps:**
1. Download the latest `itlwm.kext` from the [OpenIntelWireless/itlwm](https://github.com/OpenIntelWireless/itlwm) repository.
2. Place it in `EFI/OC/Kexts/`.
3. Add it to your `config.plist` under **Kernel → Add**.
4. Download and run the **HeliPort** app to connect to networks.
5. **Important:** Do **not** use `AirportItlwm.kext` on macOS 26.7 — it is currently unstable.

---

## ⚠️ Important Notes

1. **Sanitize your config.plist** — Replace `MLB`, `SystemUUID`, and `ROM` with your own values before using.
2. **Don't use this EFI as-is** — Every machine is different. Use this as a reference.
3. **Reset NVRAM** after making changes to your EFI.
4. **Back up your working EFI** before experimenting.
5. **KDK is mandatory** — For OCLP-Mod patches to work on macOS 26.7, you must manually install the matching KDK for your build.

---

## 🔗 Resources

- [Dortania OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/) — The Hackintosh Bible
- [OCLP-Mod GitHub](https://github.com/laobamac/OCLP-Mod) — Root patcher (archived)
- [Dortania KDK Support](https://github.com/dortania/KdkSupportPkg) — KDK downloads
- [itlwm GitHub](https://github.com/OpenIntelWireless/itlwm) — Intel Wi-Fi driver
- [RealtekCardReader GitHub](https://github.com/0xFireWolf/RealtekCardReader) — SD card driver
- [Dell Latitude 5410 Support](https://www.dell.com/support/home/en-us/product-support/product/latitude-14-5410-laptop/docs)

---

## 🙏 Credits

| Person / Project | Contribution |
| :--- | :--- |
| **Rohtu** | Inspiration to try |
| **Dortania** | The OpenCore guide |
| **Acidanthera** | OpenCore & kexts |
| **laobamac** | OCLP-Mod |
| **0xFireWolf** | RealtekCardReader |
| **OpenIntelWireless** | itlwm + HeliPort |
| **Hackintosh Community** | Keeping it alive |

---

## 🏁 Final Words

> "You don't need a Mac to run macOS. You need patience, Google, and the willingness to try something stupid."

— Chirag S Shetty, 17

**Built with frustration, caffeine, and a broken screen.**
