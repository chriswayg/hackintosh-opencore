# Hackintosh on Gigabyte Gigabyte B360 M Aorus Pro

## Installed Monterey 12.1
- Followed the [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) (Guide updated to 0.7.5 at the time and referenced the OpenCore `Configuration.pdf` for version 0.7.7).
- Relevant options chosen based on this documentation and the hardware are mostly noted below.

### Specs
* CPU: Intel Core i5-9400 CPU @ 2.90GHz 6-Core (Coffee Lake)
* MB: Gigabyte B360 M Aorus Pro
* RAM: 16GB HyperX Fury 3200MHz DDR4
* SSD: Kingston 480GB A400 SATA 2.5"
* GPU: Sapphire Radeon Toxic R9 280X with dual 1080p monitors
* WIFI: Fenvi FV-T919 (Broadcom BCM94360CD)

### Working
- Audio, Video, Ethernet, NVRAM, Wifi
- Messages, iCloud
- All USB2 & USB3 ports
- Sleep
- Upgrading to Monterey 12.2 worked smoothly

## BIOS settings

### Disable
- [x] Fast Boot
- [x] Secure Boot
- [x] Serial/COM Port
- [x] VT-d (can be enabled if you set DisableIoMapper to YES)
- [x] CSM
- [ ] CFG Lock (not available in BIOS, must enable `AppleXcpmCfgLock`)
	 
### Enable
- [ ] VT-x
- [x] Above 4G decoding
- [ ] Hyper-Threading
- [ ] Execute Disable Bit
- [x] EHCI/XHCI Hand-off
- [x] OS type: Windows 8.1/10 UEFI Mode
- [ ] DVMT Pre-Allocated(iGPU Memory): 64MB
- [x] SATA Mode: AHCI

## OpenCore Auxiliary Tools (OCAT)
Used [GitHub: OpenCore Auxiliary Tools](https://github.com/ic005k/QtOpenCoreConfig) to create initial config, while cross checking each setting with *Dortania's OpenCore Install Guide* 

- Initialize EFI with Database > `Desktop_8th-9thGen_Coffee_Lake_iMac19,1.plist`


## Edit config.plist

### NVRAM

- `boot-args -v debug=0x100 debug=0x100 alcid=1` for debugging and audio

### Device Properties
- `AAPL,ig-platform-id 0300913E` the iGPU is only used for compute tasks and doesn't drive a display

### Kernel - Quirks
- `AppleXcpmCfgLock Yes`

### Misc - Security 
- `ScanPolicy 983299`

### Platform Info

[Platform Info](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo)

- For setting up the SMBIOS info, instead of using the GenSMBIOS application, just i used the built-in Generator in OCAT.
- Click Generate once (near the SystemProductName field)

### UEFI - APFS
- `MinDate -1`
- `MinVersion -1`

## Create USB Installer & install

- Download latest Monterey (requires python):

```
mkdir -p ~/macOS-installer && cd ~/macOS-installer && curl https://raw.githubusercontent.com/munki/macadmin-scripts/main/installinstallmacos.py > installinstallmacos.py && sudo python installinstallmacos.py
```

- Use [GitHub - TINU: The open tool to create bootable macOS installers.](https://github.com/ITzTravelInTime/TINU) as a GUI for the `createinstallmedia` command

## Post-install

### Map USB Ports using USBMap
Python script for mapping USB ports in macOS and creating a custom injector kext.

https://github.com/corpnewt/USBMap


### Debugging

- Initially with all recommended debugging settings enabled, which were lowered after all is working

### Multi-Boot

- this configuration also successfully boots my previous Mojave 10.14.6 installation using the previously used Serial for AppleID consistency

### SMBIOS on Github 

In the config.plist my personal "Serial Number", "Board Serial Number" and "SmUUID" which are unique SMBIOS credentials have been changed and randomized newly before uploading, because they should not be revealed in public. They are unique for each system and are mandatory for activation of iMessage and FaceTime.
