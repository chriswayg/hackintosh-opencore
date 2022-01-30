# Hackintosh with OpenCore

## Hackintosh configurations using OpenCore

+ MB: Acer Aspire 4741 332G25Mn | CPU: Core i3-350M | GPU: Intel HD Graphics Arrandale | RAM: 4GB DDR3 1066MHz | SSD: WD 240GB | OS: High Sierra
+ MB: Asus H81M-D | CPU: Core i5-4460 | GPU:  Intel HD Graphics 4600 | RAM: 16GB  DDR3 1333MHz | SSD: WD 120GB | OS: Catalina
+ MB: GA-EP45-UD3L | CPU: Core 2 Quad Q9400 | GPU: Asus GeForce GTX 660Ti | RAM: 8GB G.SKILL 1333MHz | HD: 3TB ST3000DM001 | OS: High Sierra
+ MB: GA-Z87X-OC Force | CPU: Core i7-4770K | GPU: Sapphire Radeon R9-280X | RAM: 16GB G.SKILL 1600MHz | SSD: Crucial M550 256GB | OS: Mojave
+ MB: Gigabyte B360 M Aorus Pro | CPU: Core i5-9400 | GPU: Sapphire Radeon R9 280X | RAM: 16GB HyperX 3200MHz | SSD: Kingston 480GB | WIFI: Fenvi FV-T919 | OS: Monterey

#### To be added

- MB: Gigabyte B460 M Aorus Pro | CPU: Core i9-10900 | GPU: iGPU only, Nvidia disabled | RAM: 16GB | SSD: 250GB | OS: Monterey | Multiboot

### Check if everything is working

Use the [Hackintosh Checklist](Hackintosh_Checklist.md)

## Downloads

### OpenCore

* [GitHub - acidanthera/OpenCorePkg: OpenCore bootloader](https://github.com/acidanthera/OpenCorePkg)

### Current Tools

- Create EFI, configure and update Opencore: [GitHub - ic005k/QtOpenCoreConfig: OpenCore Auxiliary Tools OpenCore Configurator OCAT](https://github.com/ic005k/QtOpenCoreConfig)
- Plist Editor: [GitHub - ic005k/PlistEDPlus: plist editor](https://github.com/ic005k/PlistEDPlus)
- USB Port Mapper: [GitHub - corpnewt/USBMap: Python script for mapping USB ports in macOS and creating a custom injector kext.](https://github.com/corpnewt/USBMap) (requires Python)
- Python: [Download Python | Python.org](https://www.python.org/downloads/)
- Create USB Installer: [GitHub - TINU: The open tool to create bootable macOS installers.](https://github.com/ITzTravelInTime/TINU) a GUI for the `createinstallmedia` command (macOS only)

### Common Kexts

* [acidanthera/VirtualSMC · GitHub](https://github.com/acidanthera/VirtualSMC/releases)
* [acidanthera/Lilu · GitHub](https://github.com/acidanthera/Lilu/releases)
* [acidanthera/WhateverGreen · GitHub](https://github.com/acidanthera/WhateverGreen/releases)
* [acidanthera/AppleALC: Native macOS HD audio](https://github.com/acidanthera/AppleALC)
* [Releases · Sniki/OS-X-USB-Inject-All · GitHub](https://github.com/Sniki/OS-X-USB-Inject-All/releases)

## Upgrade to a new release of OpenCore

### Upgrade OpenCore manually

* [Updating OpenCore and macOS | OpenCore Post-Install](https://dortania.github.io/OpenCore-Post-Install/universal/update.html#updating-opencore-and-macos)

### Upgrade using OpenCore Auxiliary Tools (OCAT)

* keep a working EFI backup on a USB-Stick
* Refer to [OpenCorePkg/Differences.pdf at master · acidanthera/OpenCorePkg · GitHub](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Differences/Differences.pdf) of the most recent release
* Use *OpenCore Auxiliary Tools (OCAT)* for semi-automated upgrades: [Updating OpenCore and Kexts with OCAT](https://github.com/5T33Z0/OC-Little-Translated/blob/main/D_Updating_OpenCore/README.md#updating-opencore-and-kexts-with-ocat)

## Notes

The EFI folder and config.plist are just provided for reference for those who have similar hardware. Please assemble your own EFI folder according to the [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/). 

### SMBIOS on Github

In the `config.plist` my personal "Serial Number", "Board Serial Number" and "SmUUID" which are unique SMBIOS credentials have been blanked or randomized before uploading, because they should not be revealed in public. They are unique for each system and are mandatory for activation of iMessage and FaceTime.

### Deprecated Tools

- [Hackintool - InsanelyMac Forum](https://www.insanelymac.com/forum/topic/335018-hackintool-v283/) (mainly used for USB mapping)
  - [Download Hackintool](http://headsoft.com.au/download/mac/Hackintool.zip)
  - [headkaze/Hackintool: The Swiss army knife of vanilla Hackintoshing](https://github.com/headkaze/Hackintool)
- [GitHub - rusty-bits/OC-tool: Shell script that builds an OpenCore EFI folder from an OpenCore config.plist](https://github.com/rusty-bits/OC-tool) (replaced by OCAT which has more features)
- [PlistEdit Pro – Advanced Mac plist editor](https://www.fatcatsoftware.com/plisteditpro/) (nice, but commercial)
