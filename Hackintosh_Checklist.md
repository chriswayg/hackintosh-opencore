# Hackintosh Checklist - What's working?

## Desktop and General

### OpenCore Booting

- [ ] Correct OS choices shown in OpenCore Menu/GUI
- [ ] Keyboard shortcuts working (see details below)
  * CMD+V — verbose mode. 
- [ ] NVRAM working [Verifying if you have working NVRAM](https://dortania.github.io/OpenCore-Post-Install/misc/nvram.html#verifying-if-you-have-working-nvram)
  - Apple -> System Preferences -> Startup Disk uses NVRAM.
- [ ] Security (especially SIP) use [Menu Bar SIP Detector](https://github.com/ITzTravelInTime/MenuBarSIPDetector) 
- [ ] FileVault
- [ ] Multibooting

### Display

- [ ] Display via HDMI
- [ ] Display via DisplayPort
- [ ] Display via DVI
- [ ] Resolution
- [ ] Refresh rates
- [ ] Multimonitor displays

### Graphics Acceleration

- [ ] dGPU dedicated GPU
  * In Terminal: `gfxutil -f GFX0` or check in IORegistryExplorer
- [ ] iGPU internal GPU
  * In Terminal: `gfxutil -f IGPU` or check in IORegistryExplorer
- [ ] QE/CI (full acceleration requires both Quartz Extreme and Core Image)
  - Check for transparent menu bar and fast smooth UI.
- [ ] VDA (Video Decode Acceleration framework)
  - Hackintool -> System -> System -> VDA Decoder (should show 'fully supported')
- [ ] Metal
  - System Information -> Graphics/Displays -> Metal: Supported
  - GLView
  - Geekbench -> Compute -> Metal

### Audio

- [ ] Audio out (Audio MIDI Setup) 
- [ ] Audio in 
- [ ] Frontpanel audio connectors
- [ ] Audio over HDMI
- [ ] Audio quality

### Sleep & Power

- [ ] Manual Sleep (Apple menu -> Sleep)
- [ ] Auto Sleep (System preferences -> Energy Saver)
- [ ] Wake by keyboard
- [ ] Wake by mouse/trackpad
- [ ] Sleep by [Press and hold power button for 1.5 seconds](https://support.apple.com/en-us/HT201236)
- [ ] Shutdown (from Apple menu)
- [ ] Restart (from Apple menu)

### CPU

- [ ] CPU Power Management [Optimizing Power Management](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#optimizing-power-management)
  * Check with IORegistryExplorer
- [ ] Temperatures and stability with 100% CPU
  * Use Prime95 Torture Test

### Disk

- Test with *Blackmagic Disk Speedtest*

- [ ] NVMe SSD

- [ ] SATA SSD 

- [ ] TRIM support (System Information -> SATA -> SSD drive)

### Keyboard

- [ ] Option/Command correctly mapped in macOS
  * For PC Keyboards swap in: System preferences -> Keyboard -> Modifier Keys
- [ ] Fn keys working

### USB

- Use *USBMap*

- Test external drives with *Blackmagic Disk Speedtest*

- [ ] USB 2 ports

- [ ] USB 2 on USB 3 ports

- [ ] USB 3 and 3.1 ports (check transfer speed during copy)

- [ ] USB C ports

- [ ] SD Card Reader 

- [ ] Camera (Photo Booth, Facetime, Zoom)

- [ ] Fingerprint reader

### ThunderBolt

- [ ] File transfer
- [ ] Display

### Ethernet

- [ ] Gigabit LAN (System preferences -> Network -> Ethernet -> Advanced -> Hardware -> Speed should be 1000baseT)
- [ ] 2.5GBase-T (especially on Comet Lake and above boards)
- [ ] 10GBase-T (Aquantia with updated firmware)

### Wifi & Bluetooth

- [ ] Wifi transmission speed (Option Click -> Wifi menu bar icon -> check Tx Rate)
- [ ] Bluetooth devices (trackpad, mouse, keyboard, headset)
- [ ] AirDrop (test with iDevices)
- [ ] AirPlay to Mac (macOS Monterey or later, test with iOS 14 or later devices)
  * tap the AirPlay icon on your Apple device to share videos to your Hackintosh
- [ ] Handoff [System requirements for Continuity](https://support.apple.com/en-us/HT204689) and [Use Continuity](https://support.apple.com/en-us/HT204681) which requires macOS Catalina & iOS 13+
- [ ] [Sidecar](https://support.apple.com/en-us/HT210380) requires macOS Catalina or later and a compatible iPad using iPadOS 13 or later.

### OS Features

- [ ] iMessage, FaceTime, App Store, iTunes Store
- [ ] DRM support (iTunes Movies, Apple TV+, Amazon Prime and Netflix, and others)

## Laptop Specific

additional checks relevant for Notebooks including MacBooks with Legacy Patchers

### Display

- [ ] Backlight setting
- [ ] Backlight sensor
- [ ] Backlight Fn keys

### Audio

- [ ] Speaker (built-in)
- [ ] Microphone (built-in)

### Sleep & Power

- [ ] Sleep by close lid
- [ ] Sleep by close lid with external display
- [ ] Wake by open lid

### Battery

- [ ] Showing percentage
- [ ] Showing capacity/health
  * coconutBattery
- [ ] Charge plug/unplug detected

### Trackpad

- [ ] Basic functions
- [ ] Gestures

---

## OpenCore Boot Key Combinations

* [Mac startup key combinations](https://support.apple.com/en-us/HT201255)
* Enable `KeySupport` &  `PollAppleHotKeys` in Config.plist.
* For PC keyboard: enable `KeySwap`. 
* Keys can be pressed after power on or when OpenCore Picker is shown.
  * CMD+V — verbose mode.
  * CMD+S — single user mode.
  - CMD+R — boot into macOS recovery partition.
  - CMD+OPT+P+R — reset NVRAM. 
  * OPT or ESC or Zero — at startup to show OpenCore Picker
  * CTRL+ENTER at highlighted boot picker to set default boot option

## Tools

- System Integrity Protection: [menu bar app that displays the current status of SIP](https://github.com/ITzTravelInTime/MenuBarSIPDetector)
- GLview: [OpenGL Extensions Viewer](http://www.realtech-vr.com/home/glview)
- Metal benchmark: [Geekbench](https://www.geekbench.com)
- Disk Speedtest: [‎Blackmagic Disk Speed Test](https://apps.apple.com/us/app/blackmagic-disk-speed-test/id425264550)
- Battery checker: [coconutBattery](https://www.coconut-flavour.com/coconutbattery/) useful for Laptops
- USB Port Mapper: [USBMap: Python script for mapping USB ports in macOS](https://github.com/corpnewt/USBMap) 
- System Info: [Hackintool](https://github.com/headkaze/Hackintool)
- IORegistryExplorer [IORegistryClone](https://github.com/khronokernel/IORegistryClone/blob/master/ioreg-302.zip)
- CPU Torture Test: [Prime95](https://www.mersenne.org/download/)

## Links

- [OpenCore Post-Install | OpenCore Post-Install](https://dortania.github.io/OpenCore-Post-Install/)
  - covers iGPU, Audio, Sleep,  Power Management, USB mapping, NVRAM, Security, Battery, Multibooting, DRM, iMessage, etc.
- [OpenCore Reference Manual ](https://dortania.github.io/docs/latest/Configuration.html)
