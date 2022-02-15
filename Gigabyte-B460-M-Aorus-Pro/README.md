# Hackintosh on Gigabyte B460 M Aorus Pro

![](Monterey_Hackintosh_B460M_Screenshot.png)

## Hackintosh workflow

- Followed the worflow described in my [Opencore Visual Beginners Guide](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/), which is used alongside [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) (with reference to the OpenCore `Configuration.pdf` for version 0.7.7)
- Relevant options chosen based on the applicable hardware are mostly noted below.

### Specs

* CPU: Intel Core i9-10900 (10-Core Coffee Lake)
* MB: Gigabyte B460 M Aorus Pro
* RAM: 16GB Corsair DDR4
* SSD: 250GB SATA 2.5"
* iGPU: Intel UHD Graphics 630
* dGPU disabled: GeForce GTX 1650 Super
* Ethernet: Intel GbE LAN chip
* WIFI: none
* Audio: Realtek ALC1200
* Monitor main: ASUS TUF Gaming VG259QM (DisplayPort)
* Monitor secondary: ASUS VZ229H (HDMI)
* OS: Monterey 12.2, multiboot with Windows 10 Pro
* OpenCore 0.7.7

### Working

- iGPU with 2 monitors, Audio, Ethernet, USB ports, Multiboot via BIOS menu

### Issues

- Multiboot: Windows 10 frequently changes the BIOS setting CSM from disabled to enabled.
- Dual Monitors: If macOS is booted with both monitors switched on the HDMI monitor glitches and becomes unreadable. Current workaraound is to boot with the HDMI monitor only and then to plug in the DisplayPort monitor. In macOS both monitors are set to 60 Hz which improved the usability.

## BIOS settings

### Disable

- [x] Serial/COM Port
- [x] VT-d (can be enabled if DisableIoMapper is set to YES in OpenCore)
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

- Initialize EFI with Database > `Desktop_10thGen_Comet_Lake_iMac20,2.plist`

## Edit config.plist

Almost all presets loaded by OCAT are identical to the OpenCore Install Guide. Only changes will be noted below.

### ACPI and Quirks

- removed `SSDT-PMC.aml` as it is not needed

- unchecked ResetLogoStatus

### NVRAM

Disable dGPU, enable audio and debugging:

- `boot-args    -v -wegnoegpu alcid=1 debug=0x100 keepsyms=1` 

### Device Properties

Used when the Desktop iGPU is used to drive a display

- `AAPL,ig-platform-id 07009B3E` 

This only enabled the DisplayPort. In order to enable the HDMI port, I had to add additional framebuffer data. The DVI port has not been tested yet.

### Kernel - Add

- Added `IntelMausi.kext`for Intel Ethernet. 

- Not yest tested`CPUFriend.kext` and `CPUFriendDataProvider.kext` 

- Added the USB related kexts described in Post-Install.

### Kernel - Quirks

- `AppleXcpmCfgLock   No` (optional, as set in BIOS already)

### Misc - Security

Hide EFI and external from boot menu. We do not want to show Windows either, as it should be booted via BIOS or using the rEFInd Boot Manager.

- `ScanPolicy 983299`

### Platform Info

[Desktop Comet Lake](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo)

- Using iMac20,2 for i9-10850K and higher
- For setting up the SMBIOS info, I used the built-in SMBIOS generator in OCAT, (instead of using the *GenSMBIOS* application). - Click *Generate* once (near the SystemProductName field)
- Separately randomized before uploading to Github. These need to be changed before using the EFI.

## Create USB Installer & install

- Download latest Monterey 12.2 (requires python):

```
mkdir -p ~/macOS-installer && cd ~/macOS-installer && curl https://raw.githubusercontent.com/munki/macadmin-scripts/main/installinstallmacos.py > installinstallmacos.py && sudo python installinstallmacos.py
```

- Use [GitHub - TINU: The open tool to create bootable macOS installers.](https://github.com/ITzTravelInTime/TINU) as a GUI for the `createinstallmedia` command

## Post-install

### Map USB Ports

- Using USBTool from within Windows: [GitHub - USBToolBox/tool: the USBToolBox tool](https://github.com/USBToolBox/tool)

- Add `XHCI-unsupported.kext` (test, if it may not be needed)

- Add`USBToolBox.kext and the `UTBMap.kext` previously created in Windows. - I had to rework it, as the USB3 ports were not yet working with the generated kext. 

- Currently mapped: Top Front: 2 x with both USB2 & 3, Rear Top: 2 x USB2 only, Rear Middle: USB-C & USB3, Rear Down: 2 x USB3 only.

### Debugging

- Initially configured with all recommended debugging settings enabled.
