
# Dell Latitude 5410 Hackintosh — macOS 26 "Tahoe"

[![OpenCore](https://img.shields.io/badge/OpenCore-1.0.0-blue)](https://github.com/acidanthera/OpenCorePkg)
[![macOS](https://img.shields.io/badge/macOS-26_Tahoe-red)](https://www.apple.com/macos)
[![Status](https://img.shields.io/badge/Status-Working-brightgreen)]()

> macOS 26 "Tahoe" running on a Dell Latitude 5410 with OpenCore. Intel i5-10310U, UHD 620, 16GB RAM. Built by a 17-year-old who broke his screen and kept going.

---

## 📋 Hardware Specifications

| Component | Model |
|-----------|-------|
| **Laptop** | Dell Latitude 5410 |
| **CPU** | Intel Core i5-10310U (10th Gen Comet Lake) |
| **GPU** | Intel UHD 620 |
| **RAM** | 16GB DDR4 |
| **Storage** | NVMe SSD (internal) |
| **Audio** | Realtek ALC3204 (Intel SST) |
| **Display** | 1366×768 (originally 1080p — pen incident) |
| **Wi-Fi/BT** | Intel AX201 |
| **Ethernet** | Intel I219-LM |
| **Bootloader** | OpenCore 1.0.0+ |

---

## ✅ What Works

| Feature | Status |
|---------|--------|
| macOS 26 Tahoe | ✅ Fully functional |
| Intel UHD 620 Graphics | ✅ Full acceleration (no lag) |
| Wi-Fi (itlwm + HeliPort) | ✅ Working |
| Ethernet | ✅ Working |
| Bluetooth | ✅ Working |
| USB Ports (mapped) | ✅ Working |
| Apple ID / iCloud / App Store | ✅ Working (regenerated SMBIOS) |
| Dual-boot (Windows 11) | ✅ Peace treaty signed |
| Artificial Notch | ✅ Added (cosplay mode) |
| Battery Management | ✅ Working |
| Sleep/Wake | ✅ Working |

---

## ❌ What Doesn't Work (Yet)

| Feature | Status | Notes |
|---------|--------|-------|
| Intel SST Audio | ❌ Broken | Use Bluetooth/USB audio as workaround |
| iMessage / FaceTime | ❌ WIP | Serial/ROM issue — being investigated |
| HDMI | ❌ Untested | Probably needs a sacrifice |
| Built-in Mic | ❌ Broken | Same as audio |

---

## 📖 The Full Story

This wasn't a smooth install. It involved:

- **47+ config.plist rebuilds**
- **A shattered screen** (pen incident — yes, really)
- **Two weeks at the Dell service center**
- **A lost macOS partition**
- **A 40GB iCloud Notes cache bomb** that nearly killed the system
- **Apple ID serial roulette** (my serial was used by 500 other Hackintoshes)

But it works now.

Read the full 2,358-word saga here: [`STORY.md`](STORY.md)

---

## 🛠️ Tools Used

- [OpenCore](https://github.com/acidanthera/OpenCorePkg) — Bootloader
- [OpenCore Simplify](https://github.com/lzhoang2801/OpCore-Simplify) — Hardware detection
- [OCAT](https://github.com/ic005k/OCAuxiliaryTools) — Config.plist editor
- [USBToolBox](https://github.com/USBToolBox/tool) — USB port mapping
- [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) — Serial generator
- [itlwm](https://github.com/OpenIntelWireless/itlwm) + [HeliPort](https://github.com/OpenIntelWireless/HeliPort) — Wi-Fi
- [HoRNDIS](https://github.com/jwise/HoRNDIS) — USB tethering in recovery
- [modGRUBShell.efi](https://github.com/datasone/grub-mod-setup_var) — BIOS patching

---

## 📂 Repository Structure 
dell-latitude-5410-hackintosh-macos-tahoe-26/
├── README.md # You're here
├── STORY.md # Full 2,358-word saga
├── EFI/ # OpenCore EFI (sanitized)
│ ├── OC/
│ │ ├── config.plist
│ │ ├── ACPI/
│ │ ├── Drivers/
│ │ ├── Kexts/
│ │ └── Resources/
│ └── BOOT/
├── tools/ # Tool links and notes
└── screenshots/ #proof
---

## ⚠️ Important Notes

1. **Sanitize your config.plist** — Replace `MLB`, `SystemUUID`, and `ROM` with your own values.
2. **Don't use this EFI as-is** — Every machine is different. Use it as a reference.
3. **Reset NVRAM** after making changes.
4. **Back up your working EFI** before experimenting.

---

## 🔗 Resources

- [Dortania OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/) — The Hackintosh Bible
- [Dell Latitude 5410 Specs](https://www.dell.com/support/home/en-us/product-support/product/latitude-14-5410-laptop/docs)
- [Intel UHD 620 Guide](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/comet-lake.html)

---

## 🙏 Credits

- **Rohtu** — For the inspiration
- **Dortania** — For the OpenCore guide
- **Acidanthera** — For OpenCore and kexts
- **The Hackintosh Community** — For keeping this alive

---

## 📜 License

This project is for educational purposes. Use at your own risk.

---

## 🏁 Final Words

> "You don't need a Mac to run macOS. You need patience, Google, and the willingness to try something stupid."

— Chirag S Shetty, 17

---

**Built with frustration, caffeine, and a broken screen.**
