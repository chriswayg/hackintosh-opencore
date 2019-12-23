# Hackintosh on Gigabyte GA-Z87X-OC Force
## Switch to OpenCore from Clover: Z87, i7-4770K, R9-280X running Mojave
Generally followed the [Opencore Vanilla Desktop Guide](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/) and the OpenCore Configuration.pdf - The parts I configured different from the Guide are mostly noted below.

### Specs
* CPU: Intel Core i7-4770K @ 3.50GHz 4-Core Processor
* MB: Gigabyte GA-Z87X-OC Force
* RAM: 4x8GB G.SKILL Ripjaws X Series DDR3 1600
* SSD: Crucial M550 256GB 2.5"
* GPU: Sapphire Radeon Toxic R9 280X with dual 1080p monitors
* WIFI: TP-LINK TL-WDN4800

### Working
- Audio, Video, Ethernet, USB, NVRAM, Wifi, both Ethernet ports
- Messages, iCloud
- USB2 & USB3 ports
- Sleep (somewhat)
- upgrading to 10.14.6 and security updates ran smoothly
- press Option key to see OpenCore boot menu

## Download OpenCore & Tools
* [acidanthera/OpenCorePkg: OpenCore front end](https://github.com/acidanthera/OpenCorePkg)
* [acidanthera/AppleSupportPkg Drivers · GitHub](https://github.com/acidanthera/AppleSupportPkg/releases)

* [Hackintool - InsanelyMac Forum](https://www.insanelymac.com/forum/topic/335018-hackintool-v283/)
	* [Download Hackintool](http://headsoft.com.au/download/mac/Hackintool.zip)
	* [headkaze/Hackintool: The Swiss army knife of vanilla Hackintoshing](https://github.com/headkaze/Hackintool)
* [PlistEdit Pro – Advanced Mac plist editor](https://www.fatcatsoftware.com/plisteditpro/)

## BIOS settings
### Disable
	- [x] Fast Boot
	- [x] CSM
	- [ ] CFG Lock (MSR 0xE2 write protection)
### Enable
	- [x] VT-x
	- [x] Hyper Threading
	- [x] Execute Disable Bit
	- [x] EHCI/XHCI Hand-off
	- [x] OS type: other OS (otherwise no second monitor)

## Mount EFI
Used Hackintool to mount EFI

## Download Kexts & UEFI Shell
* [acidanthera/Lilu · GitHub](https://github.com/acidanthera/Lilu/releases)
* [acidanthera/VirtualSMC · GitHub](https://github.com/acidanthera/VirtualSMC/releases)
* [acidanthera/WhateverGreen · GitHub](https://github.com/acidanthera/WhateverGreen/releases)
* [acidanthera/IntelMausi · GitHub](https://github.com/acidanthera/IntelMausi/releases)
* [acidanthera/AppleALC: Native macOS HD audio](https://github.com/acidanthera/AppleALC)
* [RehabMan/USB-Inject-All: Kext to inject all USB ports](https://github.com/RehabMan/OS-X-USB-Inject-All)
	* [Download USBInjectAll 0.7.1 — Bitbucket](https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads/)
* [acidanthera/OpenCoreShell · GitHub](https://github.com/acidanthera/OpenCoreShell/releases)
* Install `AirPortAtheros40` for TP-LINK TL-WDN4800 from
	* [Atheros installer for macOS Mojave and Catalina - LAN and Wireless - InsanelyMac Forum](https://www.insanelymac.com/forum/files/file/956-atheros-installer-for-macos-mojave-and-catalina/)
	* or with Hackintool (Tools -> Atheros)

## Edit config.plist (Haswell section)
### Device Properties
* 0x04120004 - this is used when the iGPU is only used for compute tasks and doesn't drive a display
### Kernel
* remember to add path to kexts!
* ThirdPartyTrim: YES
### Misc - Boot
* ConsoleMode [blank]
* PollAppleHotKeys: YES (UsbKbDxe.efi did not work)
* Resolution: 1920x1080@32
### Misc - Tools
* Added UEFI Shell

## Cleaning out  Clover gunk
* deleted all clover related files

## Map USB Ports
* Used Hackingtool (USB-Info) and followed the built in guide
```
-uia_exclude_ss
-uia_exclude_hs uia_include=HS11,HS12
```
* installed `USBPorts.kext`

## Upgrading to OpenCore-X.Y.Z-RELEASE
* keep a backup on a USB-Stick
* replace `BOOTx64.efi` and `OpenCore.efi`
* replace drivers from updated AppleSupport `ApfsDriverLoader.efi`, `FwRuntimeServices.efi`, `VBoxHfs.efi`
* check for updated kexts on [Acidanthera · GitHub](https://github.com/acidanthera) or with the Hackintool (Installed Kexts - Download)
* read OpenCore Docs Differences.pdf and apply in config.plist, as needed
