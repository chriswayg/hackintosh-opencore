# Hackintosh on Aspire 4741 Laptop
Generally followed the  [Opencore Vanilla Desktop Guide](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/)  and the OpenCore Configuration.pdf

### Specs
* CPU: Intel Core i3 330M 2.13 GHz dual-core (Westmere/Arrandale)
* MB: Acer Aspire 4741-332G25Mn (2010)
* RAM: 4GB 1066 MHz DDR3
* SSD: 240GB 2.5"
* GPU: Intel HD Graphics
* WIFI: check
* OS: High Sierra

### Working
* Ethernet, Wifi,  Built-in Audio
* Video with Acceleration
* SATA SSD & DVD Drive
* Restart (works in Clover, but stuck in OpenCore)
* Shutdown
* USB Keyboard, Mouse, Memory Sticks
* Brightness controls, Audio controls (via Fn Keys)
* Plantronics USB Audio Headset
* limited VGA output - works with monitor mirroring only

### Needed kexts and fixes
* Prevent CMOS Reset - FixRTC in Clover ACPI
* Audio Realtek ALC272 with VodooHDA.kext
	* [https://sourceforge.net/projects/voodoohda/](https://sourceforge.net/projects/voodoohda/)
* Ethernet Broadcom BCM57780 Gigabit with BCM5722D.kext
* VodooPS2Controller.kext : Trackpad, Keyboard, Mouse
* Battery meter ACPIBatteryManager.kext
	* [https://github.com/RehabMan/OS-X-ACPI-Battery-Driver](https://github.com/RehabMan/OS-X-ACPI-Battery-Driver)

### Intel HD Graphics
* see: [GUIDE 1st Generation Intel HD Graphics QE/CI](https://www.insanelymac.com/forum/topic/286092-guide-1st-generation-intel-hd-graphics-qeci/)
* Files: [http://www.insanelymac.com/forum/files/file/208-1st-gen-intel-hd-graphics-kexts/](http://www.insanelymac.com/forum/files/file/208-1st-gen-intel-hd-graphics-kexts/)
* remove AppleIntelHDGraphics.kext and AppleIntelHDGraphicsFB.kext (before installation!)
* Use AppleIntelHDGraphicsFB.kext ::from:: **Single Link -** Alternate 2 - LCD+VGA LW1
* add Natit.kext ! (will not work without it)
* ::in Clover do not 'Inject Intel', but check ‘Patch VBios'::
* These are installed in S-L-E

### Not working or need drivers
* limited VGA output - works with monitor mirroring only (not extend to second monitor)
* Sleep (use DSDT?)
* Restart (works in Clover, but stuck in OpenCore)
* cannot boot into Recovery Partition (use second partition with full OS for recovery instead)
* internal Bluetooth hardware (does not exist!?)
	* works with USB dongle GMYLE
* HDMI? Audio HDMI? (not tested)
* Webcam UVC VendorID 1026 ProductID 38501 — VID 0x0402 PID 0x9665 Ali Corp Gateway Webcam
	* [http://www.insanelymac.com/forum/topic/238847-get-your-uvc-webcam-working-as-apple-isight/](http://www.insanelymac.com/forum/topic/238847-get-your-uvc-webcam-working-as-apple-isight/)
	* use external UVC camera
