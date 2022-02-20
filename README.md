# Hackintosh with OpenCore

## Hackintosh configurations using OpenCore

+ MB: Acer Aspire 4741 332G25Mn | CPU: Core i3-350M | GPU: Intel HD Graphics Arrandale | RAM: 4GB DDR3 1066MHz | SSD: WD 240GB | OS: High Sierra
+ MB: Asus H81M-D | CPU: Core i5-4460 | GPU:  Intel HD Graphics 4600 | RAM: 16GB  DDR3 1333MHz | SSD: WD 120GB | OS: Catalina
+ MB: GA-EP45-UD3L | CPU: Core 2 Quad Q9400 | GPU: Asus GeForce GTX 660Ti | RAM: 8GB G.SKILL 1333MHz | HD: 3TB ST3000DM001 | OS: High Sierra
+ MB: GA-Z87X-OC Force | CPU: Core i7-4770K | GPU: Sapphire Radeon R9-280X | RAM: 16GB G.SKILL 1600MHz | SSD: Crucial M550 256GB | OS: Mojave
+ MB: Gigabyte B360 M Aorus Pro | CPU: Core i5-9400 | GPU: Sapphire Radeon R9 280X | RAM: 16GB HyperX 3200MHz | SSD: Kingston 480GB | WIFI: Fenvi FV-T919 | OS: Monterey
+ MB: Gigabyte B460 M Aorus Pro | CPU: Core i9-10900 | GPU: Intel UHD Graphics 630 | RAM: 16GB Corsair DDR4 | SSD: 250GB SATA | OS: Monterey | Multiboot Windows

## Workflow

- All [OpenCore bootloader](https://github.com/acidanthera/OpenCorePkg) configurations are based on the (at time of installlation) current [Dortania - OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/).
- The workflow is explained in my [Opencore Visual Beginners Guide](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/) which uses GUI tools wherever possible for Hackintosh configuration, installation and maintenance.
- I check if everything is working using the [Hackintosh Checklist](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/install/hackintosh-checklist).
- To upgrade to a new release of OpenCore, follow the steps explained in [Upgrade OpenCore and Kexts](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/oc-auxiliary-tool-upgrade#upgrade-opencore-and-kexts).

### Main Tools

- Create EFI, configure and update Opencore: [OCAuxiliaryTools - AuOpenCore Auxiliary Tools and Configurator (OCAT)](https://github.com/ic005k/QtOpenCoreConfig)
- Plist Editor: [PlistEDPlus](https://github.com/ic005k/PlistEDPlus)
- USB Port Mapper: [USBMap: mapping USB ports in macOS and creating a custom injector kext](https://github.com/corpnewt/USBMap) (requires Python) and [USBToolBox](https://github.com/USBToolBox/tool) (on Windows)
- Python: [Download Python | Python.org](https://www.python.org/downloads/)

## Notes

The EFI folder and config.plist are just provided for reference for those who have similar hardware. Please assemble your own EFI folder according to the [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/). 

### SMBIOS on Github

In the `config.plist` my personal "Serial Number", "Board Serial Number" and "SmUUID" which are unique SMBIOS credentials have been blanked or randomized before uploading, because they should not be revealed in public. They are unique for each system and are mandatory for activation of iMessage and FaceTime.

### Previously used Tools

- [Hackintool - InsanelyMac Forum](https://www.insanelymac.com/forum/topic/335018-hackintool-v283/) 
  - Mainly used for USB mapping. Also useful for System Information and iGPU Framebuffer.
  - [Download Hackintool](http://headsoft.com.au/download/mac/Hackintool.zip)
  - [headkaze/Hackintool: The Swiss army knife of vanilla Hackintoshing](https://github.com/headkaze/Hackintool)
- [GitHub - rusty-bits/OC-tool: Shell script that builds an OpenCore EFI folder from an OpenCore config.plist](https://github.com/rusty-bits/OC-tool) - Replaced by OCAuxiliaryTools which has more features. - The developer also created a new iteration of OC-tool using Rust.
- [PlistEdit Pro – Advanced Mac plist editor](https://www.fatcatsoftware.com/plisteditpro/) - Nice, but commercial.
