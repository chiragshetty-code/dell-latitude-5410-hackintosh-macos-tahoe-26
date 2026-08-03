# Dell Latitude 5410 Hackintosh — macOS 26 Tahoe

**OpenCore EFI for Dell Latitude 5410 (i5-10310U, UHD 620, 16GB RAM)**

[![OpenCore](https://img.shields.io/badge/OpenCore-1.0.0-blue)](https://github.com/acidanthera/OpenCorePkg)
[![macOS](https://img.shields.io/badge/macOS-26_Tahoe-red)](https://www.apple.com/macos)
[![Status](https://img.shields.io/badge/Status-Working-brightgreen)]()

---

## 📌 Overview

This repository contains a working OpenCore EFI configuration for running **macOS 26 "Tahoe"** on a **Dell Latitude 5410** laptop.

Built by a 17-year-old who broke his screen, lost his partition, survived a 40GB iCloud cache bomb, and kept going.

---

## 💻 Hardware Specifications

| Component | Model |
|-----------|-------|
| **Laptop** | Dell Latitude 5410 |
| **CPU** | Intel Core i5-10310U (Comet Lake) |
| **GPU** | Intel UHD 620 |
| **RAM** | 16GB DDR4 |
| **Storage** | NVMe SSD |
| **Audio** | Realtek ALC3204 (Intel SST) |
| **Wi-Fi/BT** | Intel AX201 |
| **Display** | 1366×768 (originally 1080p) |
| **Bootloader** | OpenCore 1.0.0+ |

---

## ✅ What Works

| Feature | Status |
|---------|--------|
| macOS 26 Tahoe | ✅ Fully functional |
| Intel UHD 620 Graphics | ✅ Full acceleration |
| Wi-Fi (itlwm + HeliPort) | ✅ Working |
| Ethernet | ✅ Working |
| Bluetooth | ✅ Working |
| USB Ports | ✅ Working |
| Apple ID / iCloud / App Store | ✅ Working |
| Dual-boot with Windows 11 | ✅ Working |
| Sleep / Wake | ✅ Working |
| Battery Management | ✅ Working |

---

## ❌ What Doesn't Work

| Feature | Status | Workaround |
|---------|--------|------------|
| Intel SST Audio | ❌ Broken | Use Bluetooth or USB audio |
| iMessage / FaceTime | ❌ WIP | Serial/ROM issue |
| HDMI | ❌ Untested | Needs testing |
| Built-in Microphone | ❌ Broken | Same as audio |

---

## 🛠️ Tools Used

- [OpenCore](https://github.com/acidanthera/OpenCorePkg) — Bootloader
- [OCAT](https://github.com/ic005k/OCAuxiliaryTools) — Config editor
- [USBToolBox](https://github.com/USBToolBox/tool) — USB mapping
- [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) — Serial generator
- [itlwm](https://github.com/OpenIntelWireless/itlwm) + [HeliPort](https://github.com/OpenIntelWireless/HeliPort) — Wi-Fi
- [HoRNDIS](https://github.com/jwise/HoRNDIS) — USB tethering
- [modGRUBShell.efi](https://github.com/datasone/grub-mod-setup_var) — BIOS patching

---

## 📖 The Full Story

Read the complete 2,358-word saga here:  
👉 **[STORY.pdf](STORY.pdf)**

It covers:
- The pen incident (shattered screen)
- Two weeks with a museum-piece Inspiron 1420
- iCloud Notes 40GB cache bomb
- Apple ID serial roulette
- 47+ config.plist rebuilds

---

## ⚠️ Important Notes

1. **Sanitize your config.plist** — Replace `MLB`, `SystemUUID`, and `ROM` with your own values before using.
2. **Don't use this EFI as-is** — Every machine is different. Use this as a reference.
3. **Reset NVRAM** after making changes to your EFI.
4. **Back up your working EFI** before experimenting.

---

## 🔗 Resources

- [Dortania OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/) — The Hackintosh Bible
- [Dell Latitude 5410 Support](https://www.dell.com/support/home/en-us/product-support/product/latitude-14-5410-laptop/docs)

---

## 🙏 Credits

| Person / Project | Contribution |
|------------------|--------------|
| **Rohtu** | Inspiration to try |
| **Dortania** | The OpenCore guide |
| **Acidanthera** | OpenCore & kexts |
| **Hackintosh Community** | Keeping it alive |

---

## 🏁 Final Words

> "You don't need a Mac to run macOS. You need patience, Google, and the willingness to try something stupid."

— Chirag S Shetty, 17

---

**Built with frustration, caffeine, and a broken screen.**
