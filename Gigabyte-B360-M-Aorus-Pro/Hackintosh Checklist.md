# Hackintosh Checklist

## What's working?

**Working:** check-mark. **Not Working:** bold.

**Not Tested:** leave as-is. **Not applicable:** Strikethrough or delete.

### Desktop and General

#### OpenCore Booting

* [x] Correct OS choices shown in OpenCore Menu/GUI

* [x] Keyboard shortcuts working (see details below in _OpenCore Boot Key Combinations_)  
  
  * CMD+V — verbose mode _(check KeySwap)_

* [x] NVRAM working: [Verifying if you have working NVRAM](https://dortania.github.io/OpenCore-Post-Install/misc/nvram.html#verifying-if-you-have-working-nvram)  
  
  * Apple -> System Preferences -> Startup Disk (uses NVRAM).

* [x] Security (especially SIP) use _Menu Bar SIP Detector_

* [ ] ~~FileVault (if used)~~

* [x] Windows 10 and/or Linux Multi-Boot

* [ ] Recovery (macOS) Boot

* [x] Serial Number: ensure that it does not exist elsewhere, [Check Apple Coverage](https://checkcoverage.apple.com/us/en/) _(and not uploaded to Github)_
  
  #### Display

* [ ] Display via HDMI

* [ ] Display via DisplayPort

* [x] Display via DVI

* [x] Native Resolution

* [x] Refresh rates

* [ ] Multimonitor displays
  
  #### Graphics Acceleration

* [x] dGPU dedicated GPU  
  
  * In _Terminal_: `gfxutil -f GFX0` or check in _IORegistryExplorer_

* [ ] iGPU internal GPU  
  
  * In _Terminal_: `gfxutil -f IGPU` or check in _IORegistryExplorer_

* [x] QE/CI _(full acceleration requires both Quartz Extreme and Core Image)_
  
  * Check for transparent menu bar and fast smooth UI.

* [x] VDA _(Video Decode Acceleration framework)_  
  
  * _Hackintool -> System -> System -> VDA Decoder_ (should show '_fully supported_')

* [x] Metal  
  
  * _System Information_ -> Graphics/Displays -> Metal: Supported
  * _GLView_
  * _Geekbench_ -> Compute -> Metal

* [x] Intel Quick Sync, H.264 & HEVC (H.265) hardware decoding/encoding
  
  - *Intel Power Gadget > GFX* (green line) check while exporting H.264 from FCPX

* [ ] dGPU hardware acceleration
  
  #### Audio

* [x] Audio out (see in _Audio MIDI Setup_)

* [ ] Audio in

* [ ] Frontpanel audio connectors

* [ ] Audio over HDMI

* [x] Audio quality
  
  #### Sleep & Power
  
  Use *Energy Saver > Restore Defaults*
- [x] Check Hibernate Mode: `pmset -g | grep hibernatemode`

- [x] Shutdown (from Apple menu)

- [x] Restart (from Apple menu)
* [x] Manual Sleep (Apple menu -> Sleep)
- [x] [Press and hold power button for 1.5 seconds](https://support.apple.com/en-us/HT201236), select Sleep
* [x] Auto Sleep (_System Preferences_ -> Energy Saver)

* [x] Wake by keyboard

* [x] Wake by mouse/trackpad

* [ ] CPU Power Management [Optimizing Power Management](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#optimizing-power-management)
  
  * Check with _IORegistryExplorer_

* [x] Temperatures and stability with 100% CPU
  
  * Use _Prime95_ Torture Test
  
  #### Disk
  
  Test with *Blackmagic Disk Speedtest*

* [x] NVMe SSD (PCIe Gen3 or Gen4 speeds)

* [x] SATA SSD

* [x] TRIM support (_System Information_ -> SATA -> SSD drive)
  
  #### Sensors
  
    In HWMonitorSMC2

* [x] CPU

* [x] GPU

* [x] SSD, NVMe, HD

* [x] Fans
  
  #### Keyboard

* [x] Option/Command correctly mapped in macOS 
  
  * For PC Keyboards swap in: _System Preferences_ -> Keyboard -> Modifier Keys
  * Press space bar and the key left of the Spacebar. This should show Spotlight

* [x] Fn keys working (Audio Volume keys, etc.)
  
  #### USB
  
  Check with USBToolBox / Hackintool
  Test external drives with _Blackmagic Disk Speedtest_

* [x] USB 2 ports

* [x] USB 2 on USB 3 ports

* [x] USB 3 and 3.1 ports (check transfer speed during copy)

* [x] USB Type-C ports

* [ ] ~~SD Card Reader~~

* [x] Camera (Photo Booth, Facetime, Zoom)

* [ ] ~~Fingerprint reader~~

* [x] Gigabit LAN (_System Preferences_-> Network -> Ethernet -> Advanced -> Hardware -> Speed should be 1000baseT)

* [ ] ~~2.5GBase-T (especially on Comet Lake and above boards)~~

* [ ] ~~10GBase-T (Aquantia with updated firmware)~~
  
  #### Wifi & Bluetooth

* [x] Wifi transmission speed (Option Click -> Wifi menu bar icon -> check Tx Rate)

* [ ] Bluetooth devices (trackpad, mouse, keyboard, headset)

* [x] AirDrop (test with iDevices)

* [x] AirPlay to Mac (macOS Monterey or later, test with iOS 14 or later devices)  
  
  * tap the AirPlay icon on your Apple device to share videos to your Hackintosh

* [ ] Handoff [System requirements for Continuity](https://support.apple.com/en-us/HT204689) and [Use Continuity](https://support.apple.com/en-us/HT204681) which requires macOS Catalina & iOS 13+

* [ ] [Sidecar](https://support.apple.com/en-us/HT210380) requires macOS Catalina or later and a compatible iPad using iPadOS 13 or later.
  
  #### OS Features

* [x] iMessage, FaceTime, App Store, iTunes Store

* [ ] **DRM support** (iTunes Movies, Apple TV+, Amazon Prime and Netflix, and others. Test in Safari. Requires Polaris or newer GPU.)
