# 2018-Guide-to-Install-Ubuntu-desktop-13.04-on-Nexus-7-2012-and-Ubuntu-touch-15.04-on-Nexus-7-2013
2018 Guide to Install Ubuntu desktop 13.04 on Nexus 7 2012 and Ubuntu touch 15.04 on Nexus 7 2013

## Install Ubuntu desktop 13.04 on Nexus 7 2012

### 1.Tools and system requirements</h3>
- An Ubuntu machine
- Micro usb cable
- Nexus 7 2012 (wifi - grouper)
- Fastboot and ADB   
    $ sudo apt update   
    $ sudo apt install android-tools-adb android-tools-fastboot  
- raring-preinstalled-desktop-armhf+nexus7.bootimg and raring-preinstalled-desktop-armhf+nexus7.img.gz from http://old-releases.ubuntu.com/releases/13.04/

#### or
				
- A Windows machine
- Micro usb cable
- Nexus 7 2012 ver 1st gen nakasi(wifi - grouper)
- Fastboot , ADB driver ,Android SDK
- raring-preinstalled-desktop-armhf+nexus7.bootimg and raring-preinstalled-desktop-armhf+nexus7.img.gz from http://old-releases.ubuntu.com/releases/13.04/



### 2.Boot the device into bootloader
- Completely turn of the device
- Hold <kbd>volume down</kbd> button and press <kbd>power</kbd> button until screen light up
- release <kbd>power</kbd>  button
- release <kbd>volume down</kbd> button after enter bootloader menu

### 3.Unlock bootloader
- Ubuntu   
$ fastboot oem unlock  
- Windows   
$ cd to-where-your-fastboot-file  
$ fastboot oem unlock  
            

### 4.Flash image file
- Ubuntu and Windows  
$ fastboot erase boot  
$ fastboot erase userdata  
$ fastboot flash boot raring-preinstalled-desktop-armhf+nexus7.bootimg  
$ fastboot flash userdata raring-preinstalled-desktop-armhf+nexus7.img  
$ fastboot reboot  


### 5.Update sources.list to Trusty 14.04(optional)
- in nexus7 , open file /etc/apt/sources.list in gedit  
$ sudo gedit /etc/apt/sources.list  
- replace "raring" with "trusty" , and "http://ports." with "http://old-releases.ports."
- save the file
- run  
$ sudo apt-get update
- now you can install new software with "sudo apt-get install <package_name>"
*Warning : do not <code>run apt-get upgrade</code> or <code>apt-get dist-upgrade</code> .Upgrade will brake wireless and graphic driver.  
*Any sources newer than 14.04 will not work

## Install Ubuntu touch 15.04 Nexus 7 2013

### 1.Tools and system requirements
- An Ubuntu machine
- Micro usb cable
- Nexus 7 2013(wifi-flo or lte-deb)
- Fastboot and ADB
sudo apt update  
sudo apt install android-tools-adb android-tools-fastboot  
- ubuntu-device-flash and phablet-tools packages  
$ sudo apt-get update  
$ sudo apt-get install ubuntu-device-flash phablet-tools  
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
- run  
$ fastboot oem unlock</code>

### 4.Flash image file
- for wifi(flo) version  
$ sudo ubuntu-device-flash --server=http://system-image.ubports.com touch --channel=ubports-touch/15.04/devel --device=flo --bootstrap --wipe
- for lte(deb) version  
$ sudo ubuntu-device-flash --server=http://system-image.ubports.com touch --channel=ubports-touch/15.04/devel --device=deb --bootstrap --wipe  
*devel channel can be replace with stable or rc

### 5.Enabling read-write mode
- In Ubuntu pc  
$ phablet-config writable-image  
*Warning: Switching a device to read-write mode (and/or recovering from it) is an advanced feature and may result in complete data loss.It also disables automatic over-the-air delta updates. Accepting a full over-the-air update after making a device writable may undo changes you have made.

- You can disable read-write and restore automatic over-the-air updates:  
$ adb shell rm /userdata/.writable_image
