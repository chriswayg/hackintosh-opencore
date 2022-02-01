# Hackintosh on Gigabyte B460 M Aorus Pro

![](Monterey_Hackintosh_B460M_Screenshot.png)

## Installed Monterey 12.2

- Followed the [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) (Guide updated to 0.7.5 at the time and referenced the OpenCore `Configuration.pdf` for version 0.7.7).
- Relevant options chosen based on the applicable hardware are mostly noted below.

### Specs

* CPU: Intel Core i9-10900 (10-Core Coffee Lake)
* MB: Gigabyte B460 M Aorus Pro
* RAM: 16GB Corsair DDR4
* SSD: 250GB SATA 2.5"
* GPU: Intel UHD Graphics 630 (dGPU disabled: GeForce GTX 1650 Super)
* Ethernet: Intel I219-V
* WIFI: none
* Audio: Realtek ALC892
* OS: Monterey 12.2, multiboot with Windows 10 Pro
* OpenCore 0.7.7

### Working

- Audio, Video, Ethernet
- NVRAM seems to get changed by macOS in a way that prevents the BIOS 

## BIOS settings

### Disable

- [x] Serial/COM Port
- [x] VT-d (can be enabled if you set DisableIoMapper to YES)
- [x] CSM
- [x] Intel SGX
- [x] Intel Platform Trust
- [x] CFG Lock

### Enable

- [x] Above 4G decoding
- [x] EHCI/XHCI Hand-off
- [x] OS type: Windows 8.1/10 UEFI Mode
- [x] DVMT Pre-Allocated(iGPU Memory): 64MB
- [x] SATA Mode: AHCI

## Create EFI using OpenCore Auxiliary Tools

Used [GitHub: OpenCore Auxiliary Tools (OCAT)](https://github.com/ic005k/QtOpenCoreConfig) to create initial config, while cross checking each setting with *Dortania's OpenCore Install Guide* 

- Steps to take: [Generate EFI Folders using OpenCore Auxiliary Tools](https://github.com/5T33Z0/OC-Little-Translated/tree/main/F_Desktop_EFIs#generate-efi-folders-using-opencore-auxiliary-tools)
- Initialize EFI with Database > `Desktop_10thGen_Comet_Lake_iMac20,2.plist`

## Edit config.plist

### NVRAM

- `boot-args -v debug=0x100 debug=0x100 alcid=1` for debugging and audio

### Device Properties

- `AAPL,ig-platform-id 00009B3E` Used when the Desktop iGPU is used to drive a display

### Kernel - Quirks

- `AppleXcpmCfgLock Yes` (optional, as set in BIOS already)

### Misc - Security

Hide EFI and external in boot menu

- `ScanPolicy 983299`

### Platform Info

[Platform Info](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo)

- For setting up the SMBIOS info, instead of using the *GenSMBIOS* application, I used the built-in SMBIOS generator in OCAT.
- Click *Generate* once (near the SystemProductName field)

## Create USB Installer & install

- Download latest Monterey (requires python):

```
mkdir -p ~/macOS-installer && cd ~/macOS-installer && curl https://raw.githubusercontent.com/munki/macadmin-scripts/main/installinstallmacos.py > installinstallmacos.py && sudo python installinstallmacos.py
```

- Use [GitHub - TINU: The open tool to create bootable macOS installers.](https://github.com/ITzTravelInTime/TINU) as a GUI for the `createinstallmedia` command

## Post-install

### Map USB Ports using USBMap

Python script for mapping USB ports in macOS and creating a custom injector kext.

[GitHub - corpnewt/USBMap: Python script for mapping USB ports in macOS and creating a custom injector kext.](https://github.com/corpnewt/USBMap)

- not yet complete

### Debugging

- Initially configured with all recommended debugging settings enabled

### Multi-Boot

- This configuration is also supposed to be able to boot a Windows 10 installation on a separate SSD