# Hackintosh on Gigabyte GA-EP45-UD3L
## Switch to OpenCore from Clover: P45, Core 2 Q9400, GTX 660Ti, High Sierra
Generally followed the [Opencore Vanilla Desktop Guide](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/) and the OpenCore Configuration.pdf - The parts I configured different from the Guide are mostly noted below.

### Specs
* CPU: Intel Core 2 Quad (Yorkfield) Q9400 @ 2.66 GHz (OC up to 3.52 Ghz)
* MB: GA-EP45-UD3L LGA 775 (rev. 1.1 Bios F7)
* RAM: 4 x 2GB G.SKILL DDR2 1333 MHz
* HDD: 2 x 3TB Seagate Barracuda ST3000DM001
* GPU: ASUS GeForce GTX 660Ti (Nvidia GK104) with dual 1080p monitors
* macOS High Sierra Version 10.13.6 (Build 17G9016)

### Working
- Audio, Video, Ethernet, USB, NVRAM
- Nvidia Web Drivers
- Shutdown
- Reboot does not get back to the BIOS, but switches off the screen and then is stuck (was fine in Clover)
- Sleep does not work
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
  - Disabled IDE, Floppy, Paralell & Serial Ports

### Enable
	- [x] VT-x
	- [x] Hyper Threading
	- [x] Execute Disable Bit
	- [x] EHCI/XHCI Hand-off

## Mount EFI
Used Hackintool to mount EFI

## Download Kexts & UEFI Shell
* [acidanthera/Lilu · GitHub](https://github.com/acidanthera/Lilu/releases)
* [acidanthera/VirtualSMC · GitHub](https://github.com/acidanthera/VirtualSMC/releases)
* [acidanthera/WhateverGreen · GitHub](https://github.com/acidanthera/WhateverGreen/releases)
* [acidanthera/AppleALC: Native macOS HD audio](https://github.com/acidanthera/AppleALC)
* [RehabMan/USB-Inject-All: Kext to inject all USB ports](https://github.com/RehabMan/OS-X-USB-Inject-All)
* [Download USBInjectAll 0.7.1 — Bitbucket](https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads/)
* [acidanthera/OpenCoreShell · GitHub](https://github.com/acidanthera/OpenCoreShell/releases)
* [acidanthera/RTCMemoryFixup: open source kernel extension providing a way to emulate some offsets in your CMOS (RTC) memory](https://github.com/acidanthera/RTCMemoryFixup)

## Edit config.plist
* used Ivy Bridge section of Opencore Vanilla Desktop Guide as there is none for Yorkfield

#### Device Properties
* ig-platform-id: (blank) - no iGPU in Q9400

#### Kernel
* remember to add path to kexts!

#### Misc - Boot
* PollAppleHotKeys: YES
* Resolution: 1920x1080

#### Misc - Tools
* Added UEFI Shell

#### NVRAM boot-args
The OpenCore  RTC fix did not work, use RTCMemoryFixup instead.
* For RTCMemoryFixup add `tcfx_exclude=0D-7F` to the boot-args

## Emulated NVRAM
* deleted all Clover related files
* Install OpenCore LogoutHook.command in a directory that is accessible to all users! (The Guide instructs to install it to a personal User directory, which does not make much sense on a multi-user system.)
`sudo defaults write com.apple.loginwindow LogoutHook /Users/Shared/Scripts/LogoutHook.command`
* Apple recommends to use launchd jobs instead: [Customizing Login and Logout](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CustomLogin.html)

## USB Ports
* All USB2 ports are working (no USB3 on board)

## Legacy Install
* Use OpenCore BootInstall.command to install DuetPkg to drive

## Upgrading to OpenCore-X.Y.Z-RELEASE
* keep a backup on a USB-Stick configured with debug logging
* replace `BOOTx64.efi` and `OpenCore.efi`
* replace drivers from updated AppleSupport `ApfsDriverLoader.efi`, `FwRuntimeServices.efi`, `VBoxHfs.efi`
* check for updated kexts on [Acidanthera · GitHub](https://github.com/acidanthera) or with the Hackintool (Installed Kexts - Download)
* read OpenCore Docs Differences.pdf and apply in config.plist, as needed
