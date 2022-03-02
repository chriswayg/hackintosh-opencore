# Hackintosh on Gigabyte B460 M Aorus Pro

![](/Users/christian/developer/git_projects/hackintosh-opencore/Gigabyte-B460-M-Aorus-Pro/images/55ac098ba3dfc7ef4c2e1a260d2c9067f2f3c06e.jpg)

## Hackintosh workflow

- Followed the worflow described in my [Opencore Visual Beginners Guide](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/), which is used alongside [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) (with reference to the OpenCore `Configuration.pdf` for version 0.7.7)

![](/Users/christian/developer/git_projects/hackintosh-opencore/Gigabyte-B460-M-Aorus-Pro/images/dee6fb05f58eef4aff0559ecf1b7b5ef0e03db13.png)

Final Cut Pro runnig on Monterey performs well

### Specs

* CPU: Intel Core i9-10900 (10-Core Coffee Lake)
* MB: Gigabyte B460 M Aorus Pro
* RAM: 16GB Corsair DDR4
* SSD: Gigabyte 250GB SATA 2.5"
* iGPU: Intel UHD Graphics 630
* dGPU disabled: GeForce GTX 1650 Super
* Ethernet: Intel GbE LAN chip
* WIFI: not really needed. *(will possibly add Fenvi T919)*
* Audio: Realtek ALC1200
* Monitor main: ASUS TUF Gaming VG259QM (DisplayPort)
* Monitor secondary: ASUS VZ229H (HDMI)
* OS: Monterey 12.2.1, multiboot with Windows 10 Pro
* OpenCore 0.7.7, upgraded to 0.7.8

### Working

- iGPU with 2 monitors 1080p (DP & HDMI), Audio, Ethernet, all USB ports, Multiboot via BIOS menu
- Upgrade from macOS 12.2 to 12.2.1 worked smoothly without problems.
- DisplayPort monitor works up to 280Hz on macOS when used as a single monitor.

### Issues

- Planning to upgrade to RX 6600, as manually plugging the monitors from the dGPU to the iGPU for macOS and back for Windows is not optimal.

- **Dual Monitors:** If macOS is booted with both monitors switched on the DisplayPort Gaming monitor does not always stay on and has to be manually switched on. One current workaround is to boot with the HDMI monitor only and then to plug in the DisplayPort monitor. In macOS both monitors are set to 60 Hz which improved the usability.

- The above issue occurs while CSM is disabled in BIOS which is the preferred setting for a hackintosh. I also had sync issues which would effect one or both monitors, even with igfxonln=1 added (as suggested in a comment), and even when both monitors are on 60 Hz.

- When I re-**enabled CSM** the monitors responded better and I am able to boot properly with both monitors plugged in and switching on. No more sync issues either. Why CSM still has such an effect after the initial boot process is finished is a mystery to me. Somehow the bug or lack of synchronization occurs at the point when the Apple graphics drivers take over.

- The main monitor, ASUS TUF Gaming VG259QM (via DisplayPort) has issues with the BIOS when it is plugged into the iGPU that are independent of hackintosh use. Often it will not switch on and will not show the UEFI BIOS when booting. Could be related to poor BIOS firmware or poor monitor firmware or maybe the (factory provided) overclocking feature up to 280 Hz. It's not something that can be fixed with OpenCore.

- Multiboot: Windows 10 frequently changes the BIOS setting *CSM* from *disabled* to *enabled*. - Not an issue any more, as I found out that macOS actually boots better with CSM enabled on this board.

## BIOS settings

### Display

* [x] Initial Display Output - IGFX
* [x] Internal Graphics - Enabled
* [x] DVMT Pre-Allocated - 64M

![](/Users/christian/developer/git_projects/hackintosh-opencore/Gigabyte-B460-M-Aorus-Pro/images/74c9264803c5f5d8651864587b0a6ff681a4da64.jpeg)

### Disable

- [x] Secure Boot
- [x] Serial/COM Port
- [x] Intel SGX
- [x] Intel Platform Trust
- [x] CFG Lock
- [x] Wake on Lan

### Enable

- [x] Fast Boot (leads to better icon sizes in OpenCanopy with correct resolution)

![](/Users/christian/developer/git_projects/hackintosh-opencore/Gigabyte-B460-M-Aorus-Pro/images/d8ac26ba8c06e04188172f136df481192ad691d6.jpeg)

- [x] VT-d (can be enabled if DisableIoMapper* is set to *YES*)
- [x] Above 4G decoding
- [x] EHCI/XHCI Hand-off
- [x] OS type: Other
- [x] SATA Mode: AHCI
- [x] CSM - changed CSM to enabled (see Issues above)

![](/Users/christian/developer/git_projects/hackintosh-opencore/Gigabyte-B460-M-Aorus-Pro/images/41af2bfd4319b4f50851897a4ddc13cba6835328.jpeg)

## Create EFI using OpenCore Auxiliary Tools

Used [GitHub: OpenCore Auxiliary Tools (OCAT)](https://github.com/ic005k/QtOpenCoreConfig) to create initial config, while cross checking each setting with *Dortania's OpenCore Install Guide*

- Initialize EFI with Database > `Desktop_10thGen_Comet_Lake_iMac20,2.plist`

## Edit config.plist

Almost all presets loaded by OCAuxiliaryTools are identical to the OpenCore Install Guide. Only changes to relevant options chosen based on the applicable hardware will be noted below.

### ACPI and Quirks

- removed `SSDT-PMC.aml` as it is not needed

- unchecked `ResetLogoStatus`

### NVRAM

Disabled dGPU, enabled audio and optional debugging:

- `boot-args    -v -wegnoegpu alcid=1 debug=0x100 keepsyms=1` 

### Device Properties

Used when the Desktop iGPU is used to drive a display

- `AAPL,ig-platform-id   07009B3E` 

The above enabled the DisplayPort. The DVI port has not been tested yet. In order to enable the HDMI port, I had to add additional framebuffer data:

```
framebuffer-con2-alldata    0306180000080000C7030000
framebuffer-con2-enable     01000000
framebuffer-patch-enable    01000000
```

### Kernel - Add

- Added `IntelMausi.kext`for Intel Ethernet. 

- Not yet tested`CPUFriend.kext` and `CPUFriendDataProvider.kext` 

- Added the USB related kexts as described in Post-Install.

### Kernel - Quirks

- `AppleXcpmCfgLock   No` *(optional, as set in BIOS already)*

### Misc - Security

Hide EFI and external from boot menu. Windows, booted via *OpenCore Custom Mode* is shown via `OC_SCAN_ALLOW_FS_ESP`.

![](/Users/christian/developer/git_projects/hackintosh-opencore/Gigabyte-B460-M-Aorus-Pro/images/5a2674d56395f662f032e7477df9dd31b7d46881.png)

- `ScanPolicy    591107`

### Platform Info

[Desktop Comet Lake](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo)

- Using iMac20,2 for i9-10850K and higher
- For setting up the SMBIOS info, I used the built-in SMBIOS generator in OpenCore Auxiliary Tools.
  - Blanked before uploading to Github. *These need to be changed before using the EFI.*

```
PlatformInfo > SMBIOS > UpdateSMBIOSMode = Custom
OpenCore > Kernel > Quirks > CustomSMBIOSGuid = YES
```

This [boots Windows via OpenCore Custom Mode](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/advanced-topics/multi-boot-options#2.-booting-windows-via-opencore-custom-mode) in a way which makes SMBIOS updates exclusive to macOS only, avoiding a collision with existing Windows activation and custom software. 

## Create USB Installer & install

- Downloaded latest Monterey 12.2 (requires python):

```
mkdir -p ~/macOS-installer && cd ~/macOS-installer && curl https://raw.githubusercontent.com/munki/macadmin-scripts/main/installinstallmacos.py > installinstallmacos.py && sudo python installinstallmacos.py
```

- Used [GitHub - TINU: The open tool to create bootable macOS installers.](https://github.com/ITzTravelInTime/TINU) as a GUI for the `createinstallmedia` command

## Post-install

### Map USB Ports

![USB-mapped-all-MrT-05.png](/Users/christian/developer/git_projects/hackintosh-opencore/Gigabyte-B460-M-Aorus-Pro/images/fbb5ad922b15c6484f9ff3b538a602d7a7d2cf83.png)

- Tried using USBTool from within Windows: [GitHub - USBToolBox/tool: the USBToolBox tool](https://github.com/USBToolBox/tool). AddedUSBToolBox.kext and the`UTBMap.kext` previously created in Windows.

- Added `XHCI-unsupported.kext` *(test, if it may not be needed)*

- I had to rework `UTBMap.kext`, as the USB3 ports were not yet working with the generated kext. Then switched to Hackintool export and mapped some of the missing ports manually in `USBPorts.kext`using a plist editor.

- Completely mapped: Front Top: 2 x with both USB2 & 3, Rear Top: 2 x USB2 only, Rear Middle: USB-C & USB2 & 33, Rear Down: 2 x USB2 & 3. All work as intended. Checked with disk speed test:

![](/Users/christian/developer/git_projects/hackintosh-opencore/Gigabyte-B460-M-Aorus-Pro/images/72a6fe56b2d566f7a911ccada58bd2ef56348e2b.png)

### Debugging & Upgrades

- Initially configured with all recommended debugging settings enabled. Used OpenCore debugging to check on monitor resolution with OpenCanopy, which changed with or without CSM.  
- Upgraded kexts and OpenCore 0.7.7 to 0.7.8 with OCAuxiliaryTools

![](/Users/christian/developer/git_projects/hackintosh-opencore/Gigabyte-B460-M-Aorus-Pro/images/6a3422173d279b2a7930767db59b008441d57abe.png)

### 
