# Converting Dell OptiPlex 5040 to macOS 15.2 Sequoia

I got a Dell OptiPlex 5040 for a reasonable price and decided to create this repo for learning purposes in converting it into macOS 15.2 Sequoia.

## Hardware Requirements

- Wireless Keyboard & Mouse (USB Dongle)
- Monitor connected via DP or HDMI
- RJ-45 cable for internet connection
- (Optional) Fenvi T919 for WiFi & Bluetooth
- USB Drive (at least 32GB)

## Steps

### Map the USB Ports

1. Boot into Windows first and map all available USB ports. I found this YouTube guide helpful: [YouTube Guide](https://www.youtube.com/watch?v=eBaSUxQ7R9M).
2. Once you've generated the `UTBMap.kext` file, save it for later. I usually store it on a separate USB thumb drive (formatted as ExFAT) so it’s accessible in both macOS and Windows.

### Prepare the Installation USB Thumb Drive

1. Follow the steps in this guide: [OpenCore macOS Installer Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#downloading-macos-modern-os).

2. If using macOS, format the USB drive properly:

   - Open **Disk Utility**
   - Select the entire USB drive (not just a partition)
   - Click **Erase** and choose **Mac OS Extended (Journaled)**
   - This ensures that an EFI partition is created

3. Useful command-line scripts:

   ```sh
   sudo /Library/Developer/CommandLineTools/usr/bin/python3 installinstallmacos.py
   sudo /Applications/Install\ macOS\ Sequoia.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
   ```

### EFI Setup

1. Copy the EFI folder from this repository and save it to the EFI partition of your USB drive.
2. To mount the EFI partition, use the MountEFI script: [MountEFI](https://github.com/corpnewt/MountEFI).
3. Run the script:
   ```sh
   ./MountEFI.command
   ```
4. If you don’t see the EFI folder, reformat the USB drive as described in the installation step above.

### Prepare Config.plist

1. Copy `UTBMap.kext` along with `USBToolBox.kext` from the latest release here: [USBToolBox](https://github.com/USBToolBox/tool?tab=readme-ov-file).
2. Install **OCAuxiliaryTools** on macOS and update **GenSMBIOS** to generate serial numbers. Set the machine as `iMac18,1` or `iMac18,2`.
3. Update and merge all kext files.
4. If on Windows, refer to this guide for OpenCore installation: [Windows Installation Guide](https://github.com/alienator88/ASUS-TUF-Z390M-Pro-Gaming-Hackintosh-OpenCore/tree/Ventura).

## BIOS Settings

1. Disable CFG Lock, set DVMT to 64MB, and enable 4G Encoding (Above 4GB MMIO BIOS assignment):

   - Learn about CFG Lock: [CFG Lock Guide](https://dortania.github.io/OpenCore-Post-Install/misc/msr-lock.html#what-is-cfg-lock)
   - Check your BIOS version. Mine is **1.22**. Download the BIOS update here: [Dell BIOS Update](https://dl.dell.com/FOLDER08337268M/1/OptiPlex_5040_1.22.0.exe).
   - Extract Unicode values using this guide: [BIOS Extraction Guide](https://github.com/dreamwhite/bios-extraction-guide/tree/master/Dell).

2. Modify BIOS settings using `modGRUBShell.efi`:

   ```sh
   setup_var 0xAF 0x0  # Disable CFG Lock
   setup_var 0x350 0x2 # Set DVMT to 64MB
   setup_var 0x355 0x1 # Enable Above 4G Encoding
   ```

   - Video tutorial for GRUB Shell: [Watch from 4:15-4:50](https://www.youtube.com/watch?v=wcfU0xNvpDM\&t=285s).

### Additional Modifications

#### Disconnect CD Drive

#### BIOS Configuration

- **Boot Sequence**: Ensure OpenCore is selected as UEFI boot.
- **Advanced Boot**: Disable **Legacy Options ROMs**.
- **Performance**: Enable **HyperThreading**.
- **Intel Software Guard Extensions**: Disable.
- **Secure Boot**: Disable.
- **Multi-Display**: Enable (if available).
- **Integrated NIC**: Enable.
- **Serial Port**: Disable.
- **SATA Operation**: Set to **AHCI**.
- **USB Configuration**: Enable all options.
- **Virtualization Support**: Enable **Intel Virtualization Technology**.
- **Security**: Enable **CPU XD**.

## Installing macOS

1. Boot from the USB installer and press **Spacebar** to show all options. Select **Install macOS**.
2. The installation will take about **30 minutes**, with multiple reboots. Always select **Install macOS** when prompted.
3. Once in **macOS Utilities**, open **Disk Utility**:
   - Erase the target drive as **APFS with GUID Partition Map**.
   - Continue installing macOS (may take 30 mins to 1 hour).
4. Ensure the machine is connected to the internet via RJ-45.
5. Complete the macOS setup and verify everything is working.

## Tools Needed

- [USBToolBox](https://github.com/USBToolBox/tool) - Mapping USB ports
- [OpenCore (Latest Version)](https://github.com/acidanthera/OpenCorePkg)
- [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools/releases)
- [MountEFI](https://github.com/corpnewt/MountEFI)
- [UEFITool](https://github.com/LongSoft/UEFITool/releases)
- [IFR Extractor](https://github.com/LongSoft/Universal-IFR-Extractor/releases)

## References

- [Dell OptiPlex 5040 Hackintosh Guide](https://www.tonymacx86.com/threads/almost-success-dell-optiplex-5040.331274/)
- [Getting Started with OpenCore](https://dortania.github.io/OpenCore-Install-Guide/prerequisites.html#prerequisites)
- [OpenCore USB Installer Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
- [CFG Lock Guide](https://dortania.github.io/OpenCore-Post-Install/misc/msr-lock.html#turning-off-cfg-lock-manually)
- [GRUB Shell Video Tutorial](https://www.youtube.com/watch?v=wcfU0xNvpDM\&t=285s)

---


