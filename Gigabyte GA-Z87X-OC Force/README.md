# Hackintosh on Gigabyte GA-Z87X-OC Force

## OpenCore: Z87, i7-4770K, HD 7770 running Ventura

Generally followed the [Opencore Vanilla Desktop Guide](https://github.com/khronokernel/Opencore-Vanilla-Desktop-Guide/tree/0.5.6) and the OpenCore Configuration.pdf - The parts I configured different from the Guide are mostly noted below.

### Specs

* CPU: Intel Core i7-4770K @ 3.50GHz 4-Core Processor (Haswell)
* MB: Gigabyte GA-Z87X-OC Force
* RAM: 4x8GB G.SKILL Ripjaws X Series DDR3 1600
* SSD: Crucial M550 256GB 2.5"
* GPU: Generic AMD Radeon HD 7770
* WIFI: (none)

### Working

- Audio, Video, Ethernet, USB, NVRAM, one Ethernet port
- Messages, iCloud
- USB2 & USB3 ports
- Sleep (somewhat)

### Working
- Wifi (no card)
- second Ethernet port

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

Used OCAuxiliary Tools to mount EFI and edit config.plist

## Edit config.plist

### Device Properties

* 0x04120004 - this is used when the iGPU is only used for compute tasks and doesn't drive a display
  
  ### Kernel
* ThirdPartyTrim: YES
  
  ### Misc - Boot
* ConsoleMode [blank]
* PollAppleHotKeys: YES 
* Resolution: 1920x1080@32
  
  ### Misc - Tools
* Added UEFI Shell

## Map USB Ports

* Used Hackingtool (USB-Info) and followed the built in guide
  
  ```
  -uia_exclude_ss
  -uia_exclude_hs uia_include=HS11,HS12
  ```
* installed `USBPorts.kext`
