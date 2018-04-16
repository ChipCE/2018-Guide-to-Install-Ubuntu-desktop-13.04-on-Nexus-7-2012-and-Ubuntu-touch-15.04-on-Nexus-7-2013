# Guide to Install Ubuntu on nexus 7 2012/2013
Guide to Install Ubuntu desktop 13.04 on Nexus 7 2012(grouper) and Ubuntu touch 15.04 on Nexus 7 2013(flo,deb)  
Updated : 2018/04/16  

# Install Ubuntu desktop 13.04 on Nexus 7 2012

### 1.Tools and system requirements</h3>
- An Ubuntu machine
- Micro usb cable
- Nexus 7 2012 (wifi - grouper)
- Fastboot and ADB   
<code>$ sudo apt update</code>   
<code>$ sudo apt install android-tools-adb android-tools-fastboot</code>  
- raring-preinstalled-desktop-armhf+nexus7.bootimg and raring-preinstalled-desktop-armhf+nexus7.img.gz from http://old-releases.ubuntu.com/releases/13.04/
- extract the "raring-preinstalled-desktop-armhf+nexus7.img.gz" .Rename file "raring-preinstalled-desktop-armhf+nexus7.raw" to "raring-preinstalled-desktop-armhf+nexus7img".

#### or
				
- A Windows machine
- Micro usb cable
- Nexus 7 2012 ver 1st gen nakasi(wifi - grouper)
- Fastboot , ADB driver ,Android SDK
- raring-preinstalled-desktop-armhf+nexus7.bootimg and raring-preinstalled-desktop-armhf+nexus7.img.gz from http://old-releases.ubuntu.com/releases/13.04/
- extract the "raring-preinstalled-desktop-armhf+nexus7.img.gz" .Rename file "raring-preinstalled-desktop-armhf+nexus7.raw" to "raring-preinstalled-desktop-armhf+nexus7img".



### 2.Boot the device into bootloader
- Completely turn of the device
- Hold <kbd>volume down</kbd> button and press <kbd>power</kbd> button until screen light up
- release <kbd>power</kbd>  button
- release <kbd>volume down</kbd> button after enter bootloader menu

### 3.Unlock bootloader
- Connect nexus to PC via USB cable
- Ubuntu   
<code>$ fastboot oem unlock</code>  
- Windows   
<code>$ cd to-where-your-fastboot-file</code>  
<code>$ fastboot oem unlock</code>  
            

### 4.Flash image file
- Ubuntu and Windows  
<code>$ fastboot erase boot</code>  
<code>$ fastboot erase userdata</code>  
<code>$ fastboot flash boot raring-preinstalled-desktop-armhf+nexus7.bootimg</code>  
<code>$ fastboot flash userdata raring-preinstalled-desktop-armhf+nexus7.img</code>  
<code>$ fastboot reboot</code>  


### 5.Update sources.list to Trusty 14.04(optional)
- in nexus7 , open file /etc/apt/sources.list in gedit  
<code>$ sudo gedit /etc/apt/sources.list</code>  
- replace "raring" with "trusty" , and "http://ports." with "http://old-releases.ports."
- save the file
- run  
<code>$ sudo apt-get update</code>
- now you can install new software with "sudo apt-get install <package_name>"
*Warning : do not <code>run apt-get upgrade</code> or <code>apt-get dist-upgrade</code> .Upgrade will brake wireless and graphic driver.  
*Any sources newer than 14.04 will not work
  
  
  
# Install Ubuntu touch 15.04 Nexus 7 2013

### 1.Tools and system requirements
- An Ubuntu machine
- Micro usb cable
- Nexus 7 2013(wifi-flo or lte-deb)
- Fastboot and ADB  
<code>sudo apt update</code>  
<code>sudo apt install android-tools-adb android-tools-fastboot</code>  
- ubuntu-device-flash and phablet-tools packages  
<code>$ sudo apt-get update</code>  
<code>$ sudo apt-get install ubuntu-device-flash phablet-tools</code>  
*To install ubuntu-device-flash,you need to enable universe archive.
open /etc/apt/sources.list and delete the '#' at the beginning of the line  
deb http://us.archive.ubuntu.com/ubuntu/ xyz universe  
deb-src http://us.archive.ubuntu.com/ubuntu/ xyz universe  
deb http://us.archive.ubuntu.com/ubuntu/ xyz-updates universe  
deb-src http://us.archive.ubuntu.com/ubuntu/ xyz-updates universe  
*xyz is your ubuntu codename   
*if phablet-tools cannot be found you can use the deb file in this repo.

### 2.Boot the device into bootloader
- Completely turn of the device
- Hold <kbd>volume down</kbd> button and press <kbd>power</kbd> button until screen light up
- release <kbd>power</kbd>  button
- release <kbd>volume down</kbd> button after enter bootloader menu

### 3.Unlock bootloader
- Connect nexus to PC via USB cable
- run  
<code>$ fastboot oem unlock</code>

### 4.Flash image file
- for wifi(flo) version  
<code>$ sudo ubuntu-device-flash --server=http://system-image.ubports.com touch --channel=ubports-touch/15.04/devel --device=flo --bootstrap --wipe</code>
- for lte(deb) version  
<code>$ sudo ubuntu-device-flash --server=http://system-image.ubports.com touch --channel=ubports-touch/15.04/devel --device=deb --bootstrap --wipe</code>  
*devel channel can be replace with stable or rc

### 5.Enabling read-write mode
- In Ubuntu pc  
<code>$ phablet-config writable-image</code>  
*Warning: Switching a device to read-write mode (and/or recovering from it) is an advanced feature and may result in complete data loss.It also disables automatic over-the-air delta updates. Accepting a full over-the-air update after making a device writable may undo changes you have made.

- You can disable read-write and restore automatic over-the-air updates:  
<code>$ adb shell rm /userdata/.writable_image</code>
