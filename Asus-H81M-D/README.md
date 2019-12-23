# Hackintosh on Asus H81M-D

Generally followed the [Opencore Vanilla Desktop Guide](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/) and the OpenCore Configuration.pdf - The parts I configured differently from the Guide are mostly noted below.

### Specs
* CPU: Intel Core i5-4460 4-Core Processor
* MB: Asus H81M-D
* RAM: 16GB DDR3 1333MHz
* SSD: WD 120GB 2.5"
* GPU: Intel HD Graphics 4600
* WIFI: TP-LINK TL-WDN4800
* OS: Catalina

### Working
- Audio, Video, Ethernet, USB, NVRAM, Wifi, Ethernet
- Messages, iCloud
- USB2 & USB3 ports
- Sleep
- upgrading to 10.15.2 and security updates ran smoothly
- press Option key to see OpenCore boot menu
- Mouse is partially unresponive for 20 seconds on login screen

## Download Tools
* [Hackintool - InsanelyMac Forum](https://www.insanelymac.com/forum/topic/335018-hackintool-v283/)
	* [Download Hackintool](http://headsoft.com.au/download/mac/Hackintool.zip)
	* [headkaze/Hackintool: The Swiss army knife of vanilla Hackintoshing](https://github.com/headkaze/Hackintool)
* [PlistEdit Pro – Advanced Mac plist editor](https://www.fatcatsoftware.com/plisteditpro/)

## BIOS settings

### Disable
	- [x] CSM
	- [ ] CFG Lock (MSR 0xE2 write protection)

### Enable
	- [x] Fast Boot (this works nicely)
	- [x] VT-x
	- [x] Hyper Threading
	- [x] Execute Disable Bit
	- [ ] EHCI/XHCI Hand-off
	- [x] OS type: other OS

## Edit config.plist (Haswell section)
### ACPI
* create SSDT-EC.aml

### Device Properties
* use iGPU for main display

### Kernel
* ThirdPartyTrim: YES

### Misc - Boot
* PollAppleHotKeys: YES
* Resolution: 1920x1080

### Misc - Tools
* Add UEFI Shell

## Download OC-Tool and add Kexts
* [GitHub - rusty-bits/OC-tool: Shell script that builds an OpenCore EFI folder from an OpenCore config.plist](https://github.com/rusty-bits/OC-tool)
* [RehabMan/USB-Inject-All: Kext to inject all USB ports](https://github.com/RehabMan/OS-X-USB-Inject-All)
	* [Download USBInjectAll — Bitbucket](https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads/)
* add USBInjectAll.kext and SSDT-EC.aml to OC-tool/extras

## Mount EFI
Used Hackintool to mount EFI

## Map USB Ports
* Used Hackingtool (USB-Info) and followed the built in guide
```
-uia_exclude_ss
-uia_exclude_hs uia_include=HS03,HS04
```
* add `USBPorts.kext`

* Install `AirPortAtheros40` for TP-LINK TL-WDN4800
	* with Hackintool (Tools -> Atheros)

## Upgrading to OpenCore-X.Y.Z-RELEASE
* keep a backup on a USB-Stick
* check OpenCore Docs Differences.pdf and apply in config.plist, as needed
* Use OC-Tool to build the latest version from source based on config.plist
