# Hackintosh with OpenCore

## Hackintosh computers using OpenCore

+ MB: Acer Aspire 4741 332G25Mn | CPU: Core i3-350M | GPU: Intel HD Graphics Arrandale | RAM: 4GB DDR3 1066MHz | SSD: WD 240GB | OS: High Sierra
+ MB: Asus H81M-D | CPU: Core i5-4460 | GPU:  Intel HD Graphics 4600 | RAM: 16GB  DDR3 1333MHz | SSD: WD 120GB | OS: Catalina
+ MB: GA-EP45-UD3L | CPU: Core 2 Quad Q9400 | GPU: Asus GeForce GTX 660Ti | RAM: 8GB G.SKILL 1333MHz | HD: 3TB ST3000DM001 | OS: High Sierra
+ MB: GA-Z87X-OC Force | CPU: Core i7-4770K | GPU: Sapphire Radeon R9-280X | RAM: 16GB G.SKILL 1600MHz | SSD: Crucial M550 256GB | OS: Mojave
+ MB: Gigabyte B360 M Aorus Pro | CPU: Core i5-9400 | GPU: Sapphire Radeon R9 280X | RAM: 16GB HyperX 3200MHz | SSD: Kingston 480GB | WIFI: Fenvi FV-T919 | OS: Ventura
+ MB: Gigabyte B460 M Aorus Pro | CPU: Core i9-10900 | GPU: Intel UHD Graphics 630 | RAM: 16GB Corsair DDR4 | SSD: 250GB SATA | OS: Monterey | Multiboot Windows

Details are inside the Readme of each individual hackintosh project folder.

## Workflow

- All [OpenCore](https://github.com/acidanthera/OpenCorePkg) configurations are based on the current [Dortania - OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) (current at date of installlation).
- The workflow is explained in my [Opencore Visual Beginners Guide](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/) which uses GUI tools wherever possible for configuration, installation and maintenance of the Hackintosh.
- The [Hackintosh Checklist](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/install/hackintosh-checklist) is useful to verify what is working.
- The steps to upgrade to a new release of OpenCorea are explained in [Upgrade OpenCore and Kexts](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/oc-auxiliary-tool-upgrade#upgrade-opencore-and-kexts).

### Main Tools

- [OCAuxiliaryTools - OpenCore Auxiliary Tools and Configurator (OCAT)](https://github.com/ic005k/QtOpenCoreConfig) - Create EFI, configure and update Opencore.
- [PlistEDPlus](https://github.com/ic005k/PlistEDPlus) - A nice easy to use cross-platform Plist Editor.
- USB Port Mapper: [USBMap](https://github.com/corpnewt/USBMap) (requires [Python](https://www.python.org/downloads/)) , [USBToolBox](https://github.com/USBToolBox/tool) (on Windows), and *Hackintool*.
- [Hackintool](https://github.com/headkaze/Hackintool), [Download](http://headsoft.com.au/download/mac/Hackintool.zip), [Forum](https://www.insanelymac.com/forum/topic/335018-hackintool-v283/) - Mainly used for USB mapping. Also useful for System Information and iGPU Framebuffer.

## Notes

The EFI folder and config.plist are just provided for reference for those who have similar hardware. *Please assemble your own EFI folder according to the [Dortania - OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/).*

### SMBIOS on Github

In the `config.plist` my personal *"Serial Number"*, *"Board Serial Number"* and *"SmUUID"* which are unique SMBIOS credentials have been blanked or randomized before uploading, because they should not be revealed in public. They are unique for each system and are mandatory for activation of iMessage and FaceTime.

### Previously used Tools

- [OC-tool: Shell script that builds an OpenCore EFI folder from an OpenCore config.plist](https://github.com/rusty-bits/OC-tool) - I am now using OCAuxiliaryTools which is a GUI app with more features. - The developer also created a new fully featured version of OC-tool: [rusty-bits/octool: command line tool for editing an OpenCore config.plist and generating an EFI folder](https://github.com/rusty-bits/octool).
- [PlistEdit Pro – Advanced Mac plist editor](https://www.fatcatsoftware.com/plisteditpro/) - Nice, but commercial.
