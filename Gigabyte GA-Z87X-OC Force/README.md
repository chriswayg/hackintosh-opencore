# Hackintosh on Gigabyte GA-Z87X-OC Force
## Switch to OpenCore from Clover: Z87, i7-4770K, R9-280X running Mojave
Generally followed the [Opencore Vanilla Desktop Guide](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/) and the OpenCore Configuration.pdf - The parts I configured different from the Guide are mostly noted below.

### Specs
* CPU: Intel Core i7-4770K @ 3.50GHz 4-Core Processor (Haswell)
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

* Install `AirPortAtheros40` for TP-LINK TL-WDN4800 from
	* [Atheros installer for macOS Mojave and Catalina - LAN and Wireless - InsanelyMac Forum](https://www.insanelymac.com/forum/files/file/956-atheros-installer-for-macos-mojave-and-catalina/)
	* or with Hackintool (Tools -> Atheros)

## Edit config.plist
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
