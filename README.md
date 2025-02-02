![Screenshot 2568-02-02 at 12 27 37](https://github.com/user-attachments/assets/757aa09f-2544-4bd1-80e8-55246b27b735)

# OpenCore 1.0.3 Stable - macOS Sonoma 14 - Lenovo ideapad 330S-15IKB (81F5)

While the **i5-8250U** processor in this laptop is compatible with **macOS Sequoia**, This EFI **Doesn't support macOS Sequoia** due to the `AirportItlwm` and `IntelBluetoothFirmware` kext compatibility. Upgrading to Broadcom wireless card is recommended for better stability and features for current and future macOSes.
* What to do to get Sequoia Intel Wifi/Bluetooth running?
  * Workaround [OCLP AirportItlwm](https://github.com/OpenIntelWireless/itlwm/issues/1009#issuecomment-2370919270) (may not guarantee stability)
  * Bluetooth is a hit or miss [OpenIntelWireless/IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware)
  * *Alternatively upgrade to Broadcom Wlan card*

```
* I am not responsible for any damage done to your device. Use at your own risk.
* Please do some research if you concerns about features included in this EFI.
* Before continuing, you are choosing to make these modifications yourself
* if any thing goes wrong, it is your responsible for the damage that happen next.
```

## Important note

#### ***Every laptop are difference, even those with the same model number. So use this EFI as a reference and edit accordingly to your own hardware.***

### You need to generate your own SMBIOS to signin with Apple ID
Use CorpNewt's [GENSMBIOS](https://github.com/corpnewt/GenSMBIOS) to generate platforminfo using `MacBookPro15,2` (i5-8259U) as an SMBIOS

### What works
* Native OTA Updates
* Full Metal GPU Acceleration
* WiFi & Bluetooth connection
* Onboard Audio & Microphone
* Keyboard & Trackpad
* Webcam
* USB 3.0
* USB C
* SD Card reader
* HDMI Video/Audio output
* Battery read-out
* Display Brightness Control & BrightnessKeys
* Volume control keys
* Sleep & Wake
* lid Sleep & Wake

### What not works
* Airdrop & Continuity Features (Need native wificard)
* Build-in Windows control keys: Close window, Refresh, Airplane mode, Task switch, Display toggle will not work

### Untested
* 3.5mm Audio out
* Hibernation

## Known issues
* Reboot loop couple of time before successfully booting into macOS.
* Trackpad not working sometime after reboot/powerup.

## Wlan Related kext
If you have difference **Wlan card** other than Intel ([OpenIntelWireless](https://openintelwireless.github.io/) kexts were used for both WiFi and Bluetooth in this EFI)
#### **removes/excludes:**
* `AirportItlwm.kext`
* `BlueToolFixup.kext`
* `IntelBTPatcher.kext`
* `IntelBluetoothFirmware.kext`

from `EFI/OC/Kexts` folder and `config.plist` then replace with one that work for your card. otherwise Wifi&Bluetooth will not work properly or will not boot at all.

## Bios/UEFI Settings
**Configuration**
* Configuration
  * Graphic Device: `UMA Only`
  * Storage > Controller Mode: `AHCI mode`
* Security
  * Intel Platform Trust Technology: `Disabled`
  * Secure Boot: `Disable`
* Boot
  * Boot Mode: `UEFI`
  * USB Boot: `Enabled`

## Laptop Specs/Details
* Model: `Lenovo ideapad 330S-15IKB (81F5)`
* Processor: `8th gen Core i5-8250U (Kaby Lake R)`
* CPUID: `Intel(R) Core(TM) i5-8250U CPU @ 1.60GHz`
* iGPU: `intel UHD Graphic 620`
* dGPU: `AMD Radeon 535 2GB DDR5`
* Ram: `12gb 4+8 @ 2400 MHz`
* DRIVE1 HDD: `WDC WD10SPZX-24Z10T0 (WD-WX41A38DF1JN) (SATA)`
* DRIVE2 SSD: `Drive ADATA SX6000NP (2I1320041166        _00000001.) (NVMe)`
* Keyboard connection type: `PS/2`
* Trackpad connection type: `I2C`
* Audio: `Realtek ALC236 @ Intel Sunrise Point-LP PCH - High Definition Audio Controller [C1]	(PCI)`
* Audio HDMI: `Intel Kaby Lake HDMI @ Intel Sunrise Point-LP PCH - High Definition Audio Controller [C1]	(PCI)`
* Ethernet: `No connector`
* WLAN: `Intel Dual Band Wireless-AC 3165 AC HMC WiFi Adapter	(PCI)`

## Links/Guides
* https://github.com/acidanthera/OpenCorePkg (OpenCore Bootloader)
* https://dortania.github.io/OpenCore-Install-Guide/ (OpenCore Setup,Installation,Troubleshooting)
* https://openintelwireless.github.io/itlwm/ (Native Intel WiFi)
* https://openintelwireless.github.io/IntelBluetoothFirmware/ (Native Intel Bluetooth)
* https://github.com/corpnewt/GenSMBIOS (mac Serial)
