# macOS on Toshiba Satellite C50T-A052 (OpenCore Config)

This repository contains the OpenCore configuration for the Toshiba Satellite C50T-A052 Laptop for use on yours

---

## 🖥️ System Specs

| Component       | Details                                           |
|-----------------|---------------------------------------------------|
| **CPU**         | Intel Core i3-3120M (Ivy Bridge, 2.5GHz, 2C/4T)   |
| **GPU**         | Intel HD Graphics 4000                            |
| **RAM**         | 4 GB DDR3                                         |
| **Storage**     | 512 GB HDD/SSD                                    |
| **Audio**       | Realtek ALC269                                    |
| **Keyboard**    | PS/2                                              |
| **Touchpad**    | PS/2 Synaptics                                    |
| **Touchscreen** | ELAN                                              |
| **WiFi**        | Atheros AR9565                                    |
| **Bluetooth**   | Atheros QCA9565                                   |
| **Ethernet**    | Atheros 8162/8166/8168 PCI-E Fast Ethernet        |
| **USB Ports**   | 1× USB 3.0, 2× USB 2.0                            |
| **HDMI**        | Supported                                         |

---

## macOS Compatibility

| macOS Version         | Status                   | Notes                                                                        |
|-----------------------|--------------------------|------------------------------------------------------------------------------|
| **macOS 11 Big Sur**  | ✅ Fully Supported      | Best stable experience with proper acceleration and working features         |
| **macOS 12-15**       | ⚠️ Partially Supported  | Requires **OpenCore Legacy Patcher (OCLP)** for root patching and slow       |

> This laptop is **officially supported up to macOS Big Sur**, but newer versions (Monterey, Ventura, Sonoma, Sequoia) can work using **OCLP Root Patches**.

---

## ✅ Working

- ✅ Graphics acceleration (QE/CI)
- ✅ Audio (ALC269)
- ✅ HDMI output
- ✅ WiFi (AR9565)
- ✅ Ethernet (Atheros)
- ✅ Keyboard
- ✅ AirPlay and Display detection
- ✅ Sleep & Hibernate

---

## ❌ Not Working

- ❌ Bluetooth (QCA9565 not supported by macOS)
- ❌ ELAN Touchscreen (not supported by macOS)
- ❓ Touchpad (not testable, my touchpad is broken)
- ❓ DRM (not tested, expected to be broken)

---

## **Kexts**

#### ✅Core
* **VirtualSMC.kext** – Emulates Apple SMC, required for macOS boot
* **Lilu.kext** – Core plugin engine needed by many other kexts

##

#### 🖥️Graphics

* **WhateverGreen.kext** – Graphics patching for Intel/AMD/NVIDIA GPUs

##

#### 🎧Audio

* **AppleALC.kext** – Enables onboard audio via layout-id patching

##

#### 🌐Network

* **AtherosE2200Ethernet.kext** – Supports Atheros/Qualcomm wired Ethernet
* **HoRNDIS.kext** – Android USB tethering support
* **IO80211ElCap.kext + AirPortAtheros40.kext** – Enables Atheros Wi-Fi cards

##

#### 🔋CPU & Power

* **SMCProcessor.kext** – CPU sensor monitoring (used with VirtualSMC)
* **SMCSuperIO.kext** – Fan/voltage/temp monitoring (used with VirtualSMC)
* **AppleIntelCPUPowerManagement.kext** – Native CPU power management
* **AppleIntelCPUPowerManagementClient.kext** – Required client for above
* **ECEnabler.kext** – Enables Embedded Controller on laptops

##

#### ⚙️System/Other Fixes

* **AMFIPass.kext** – Bypasses AMFI (Apple Mobile File Integrity) for unsigned binaries
* **CryptexFixup.kext** – Fixes Cryptex setup for macOS 12+
* **RestrictEvents.kext** – Prevents Apple from detecting unsupported hardware
* **AutoPkgInstaller.kext** – Helps with automatic post-install scripts
* **BrightnessKeys.kext** – Enables brightness hotkeys on laptops

---

## Setup Instructions

1. **Download the OpenCore Config**
   - Download the config and place it on the EFI partition on your USB Drive formatted for macOS installer.

2. **Generate SMBIOS (MacBookPro11,5)**
   - Use [`GenSMBIOS`](https://github.com/corpnewt/GenSMBIOS) to create valid SMBIOS data:
     ```
     Model: MacBookPro11,5
     ```

3. **Install macOS Big Sur**
   - Use [macrecovery.py](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install-recovery/) or gibMacOS to fetch Big Sur.
   - Follow [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#macos-installer) for installation.

4. **For Sequoia or newer macOS**
   - After installing and booting, run **[OpenCore Legacy Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher)**.
   - Apply root patches for: MacBookPro11,5
   - Reboot and enjoy partial support and a laggy experience.

---

## Notes

- You can try upgrading the RAM to 8GB for better performance.
- For better Bluetooth/macOS support, consider replacing the WiFi+BT card with a **Broadcom-based** chip (e.g. DW1560 or BCM94360NG).
- This guide assumes **OpenCore 1.0.4 or newer**.

---

## Credits

- [Dortania OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
- [OpenCore Legacy Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher)
