I got a Dell Optiplex 5040 for a reasonable price and decided to create this repo for learning purposes in converting it into a Mac OS Version 15.2 Sequoia.

## Modification
### Disconnect CD Drive
 ### Bios Setup
   
  a. General>Boot Sqeunce>(Check OpenCore if there is) and UEFI:(storage where your gonna install the OS)
 
  b. General>Advanced Boot>Disable Legacy Options ROMs
  
  c. Performance>HyperThread Control>Enabled
  
  d. Intel Software Guard Extensions>Disabled
  
  e. Secure Boot Enabled>Disabled
  
  f. Video>Multi-Display>Enable Multi-Display(if any)
  
  g. System Configuration>Integrated NIC>Enabled
  
  h. System Configuration>Serial Port>Disabled
  
  i. System Configuration>SATA Operation>AHCI
  
  j. System Configuration>USB Configuration>Enable everything
  
  k. Virtualization Support>Virtualization>Enable Intel Virtualization Technology
  
  l. Security>CPU XD>Enabled

## Hardware:
- Wireless KB & Mouse USB Dongle
- Monitor connected through DP or HDMI
- RJ-45 cable for Internet connection 
- (Optional) Fenvi T919 for WiFi & Bluetooth
- USB Drive of at least 32GB

## Tools Needed:
- USBToolBox - Mapping USB ports of the machine - https://github.com/USBToolBox/tool
- OpenCore (Latest Version) - https://github.com/acidanthera/OpenCorePkg
- MountEFI - https://github.com/corpnewt/MountEFI
- UEFITool - https://github.com/LongSoft/UEFITool/releases
- IFR Extractor - https://github.com/LongSoft/Universal-IFR-Extractor/releases

## References:
- Primary Reference I used: https://www.tonymacx86.com/threads/almost-success-dell-optiplex-5040.331274/
- Understanding Opencore and preparing USB installer and how to do CFG lock https://dortania.github.io/OpenCore-Post-Install/misc/msr-lock.html#turning-off-cfg-lock-manually
- This Video helped me learn how to use GRUB Shell in modifying DVMT, CFG Lock, and 4G Encoding https://www.youtube.com/watch?v=wcfU0xNvpDM&t=285s
