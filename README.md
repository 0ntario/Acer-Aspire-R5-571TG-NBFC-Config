# Acer-Aspire-R5-571TG-NBFC-Config
 A custom NoteBook FanControl (NBFC) configuration profile mapping the EC registers for the Acer Aspire R5-571TG laptop.

# Acer Aspire R5-571TG Fan Control Config (NBFC)

A custom fan control configuration profile for the **Acer Aspire R5-571TG** (Intel Core i7-6500U, NVIDIA 940MX). This allows you to manually control your laptop's fan speed and set custom temperature curves using NoteBook FanControl (NBFC).

Since Acer locks the fan control in the BIOS and doesn't expose it to standard software like MSI Afterburner, this config interacts directly with the Embedded Controller (EC) to take manual control.

## ⚙️ Technical Details (EC Registers)
This profile was mapped manually using RWEverything:
* **Fan Speed Register:** `0x93` (Decimal 147) - Uses an inverted scale (00 = Max Speed, FF/CD = Min/Off)
* **Manual Override Toggle:** `0x9B` (Decimal 155) - Writes `0x00` to take control from BIOS, and `0xFF` to return it to auto.
* **Temperature Sensors:** `0xE2` and `0xE3`

## 📥 Prerequisites
The original NBFC is abandoned and may crash on modern Windows. It is highly recommended to use the active fork:
* Download **[NBFC-Revive](https://github.com/UraniumDonut/nbfc-revive/releases)**.

## 🚀 Installation
1. Install NBFC-Revive.
2. Download the `Acer_Aspire_R5-571TG_Custom.xml` file from this repository.
3. Move the `.xml` file into your NBFC configs folder: 
   `C:\Program Files\NoteBook FanControl\Configs` (or `Program Files (x86)`).
4. Open the NoteBook FanControl app.
5. Click the `...` next to "Selected config", choose **Acer Aspire R5-571TG (Custom)**, and click Apply.
6. Enable the Fan Control Service status.

## ⚠️ Troubleshooting: Windows Defender "Risky Action Blocked"
If NBFC fails to control the fan and Windows Defender throws a "Risky action blocked" notification, Windows is blocking the kernel driver used to read the EC via an Attack Surface Reduction (ASR) rule.

**To fix this:**
1. Open Windows Security > Device Security > Core Isolation details.
2. Turn off **Microsoft Vulnerable Driver Blocklist**.
3. Restart your PC. 

*(If the UI toggle is missing, run this in an Administrator PowerShell to disable the block via registry: `reg add "HKLM\SYSTEM\CurrentControlSet\Control\CI\Config" /v VulnerableDriverBlocklistEnable /t REG_DWORD /d 0 /f`)*
