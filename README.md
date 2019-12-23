# Hackintosh with OpenCore

### Hackintosh configurations using OpenCore

+ MB: Acer Aspire 4741 332G25Mn | CPU: Core i3-350M | GPU: Intel HD Graphics Arrandale | RAM: 4GB DDR3 1066MHz | SSD: WD 240GB | OS: High Sierra
+ MB: Asus H81M-D | CPU: Core i5-4460 | GPU:  Intel HD Graphics 4600 | RAM: 16GB  DDR3 1333MHz | SSD: WD 120GB | OS: Catalina
+ MB: GA-EP45-UD3L | CPU: Core 2 Quad Q9400 | GPU: Asus GeForce GTX 660Ti | RAM: 8GB G.SKILL 1333MHz | HD: 3TB ST3000DM001 | OS: High Sierra
+ MB: GA-Z87X-OC Force | CPU: Core i7-4770K | GPU: Sapphire Radeon R9-280X | RAM: 16GB G.SKILL 1600MHz | SSD: Crucial M550 256GB | OS: Mojave

#### Not yet added
+ MB: Gigabyte B360 M Aorus Pro | CPU: Core i5-9400 | GPU: GeForce GTX 1060 3GB | RAM: 16GB HYPERX 3200MHz | HD: 1TB - 500GB | OS: High Sierra

### Downloads
#### OpenCore
* [acidanthera/OpenCorePkg: OpenCore front end](https://github.com/acidanthera/OpenCorePkg)
* [acidanthera/AppleSupportPkg Drivers · GitHub](https://github.com/acidanthera/AppleSupportPkg/releases)

#### Tools
* [Hackintool - InsanelyMac Forum](https://www.insanelymac.com/forum/topic/335018-hackintool-v283/)
	* [Download Hackintool](http://headsoft.com.au/download/mac/Hackintool.zip)
	* [headkaze/Hackintool: The Swiss army knife of vanilla Hackintoshing](https://github.com/headkaze/Hackintool)
* [PlistEdit Pro – Advanced Mac plist editor](https://www.fatcatsoftware.com/plisteditpro/)
* [GitHub - rusty-bits/OC-tool: Shell script that builds an OpenCore EFI folder from an OpenCore config.plist](https://github.com/rusty-bits/OC-tool)

#### Kexts & UEFI Tools
* [acidanthera/Lilu · GitHub](https://github.com/acidanthera/Lilu/releases)
* [acidanthera/VirtualSMC · GitHub](https://github.com/acidanthera/VirtualSMC/releases)
* [acidanthera/WhateverGreen · GitHub](https://github.com/acidanthera/WhateverGreen/releases)
* [acidanthera/AppleALC: Native macOS HD audio](https://github.com/acidanthera/AppleALC)
* [RehabMan/USB-Inject-All: Kext to inject all USB ports](https://github.com/RehabMan/OS-X-USB-Inject-All)
  * [Download USBInjectAll 0.7.1 — Bitbucket](https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads/)
* [acidanthera/RTCMemoryFixup: open source kernel extension providing a way to emulate some offsets in your CMOS (RTC) memory](https://github.com/acidanthera/RTCMemoryFixup)
* `AirPortAtheros40` for TP-LINK TL-WDN4800 from
	* [Atheros installer for macOS Mojave and Catalina - LAN and Wireless - InsanelyMac Forum](https://www.insanelymac.com/forum/files/file/956-atheros-installer-for-macos-mojave-and-catalina/)
	* or with Hackintool (Tools -> Atheros)
* [acidanthera/OpenCoreShell · GitHub](https://github.com/acidanthera/OpenCoreShell/releases)

### Upgrade to OpenCore-X.Y.Z-RELEASE

#### Upgrade OpenCore manually
* keep a backup on a USB-Stick
* download latest OpenCore Package and AppleSupport
* replace `BOOTx64.efi` and `OpenCore.efi`
* replace drivers from updated AppleSupport `ApfsDriverLoader.efi`, `FwRuntimeServices.efi`, `VBoxHfs.efi`
* check for updated kexts on [Acidanthera · GitHub](https://github.com/acidanthera) or with Hackintool (Installed Kexts - Download)
* read OpenCore Docs Differences.pdf and apply in config.plist, as needed

#### Upgrade OpenCore using OC-Tool
* keep a backup on a USB-Stick
* check OpenCore Docs Differences.pdf and apply in config.plist, as needed
* download [GitHub - rusty-bits/OC-tool: Shell script that builds an OpenCore EFI folder from an OpenCore config.plist](https://github.com/rusty-bits/OC-tool)
* Use OC-Tool to build the latest version from source based on config.plist

### Note
 The EFI folder and config.plist are just provided for reference for those who have similar hardware. Please assemble your own EFI folder according to the [Opencore Vanilla Desktop Guide](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/). In the config.plist "Serial Number", "Board Serial Number" and "SmUUID" which are unique SMBIOS credentials have been blanked, because they should not be revealed in public. They are unique for each system and mandatory for activation of iMessage and FaceTime.
