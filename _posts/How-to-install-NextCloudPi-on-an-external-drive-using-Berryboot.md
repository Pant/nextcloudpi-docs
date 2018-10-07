How to install NextCloudPi on an external drive using Berryboot
===============================================================

A step by step guide to installing NextCloudPi to an external drive using [Berryboot](https://github.com/maxnet/berryboot).
In first place we need to install Berryboot, a bootloader and management tool for OS installations on your Raspberry Pi. You will choose where your NextCloud installation will reside in this part.  In the second part we will use a  specially squashfs formatted image to install the NextCloudPi

## Part 1: First time boot and choosing device to install Nextcloud to.

1. - Download [berryboot-20170527-pi2-pi3.zip](http://downloads.sourceforge.net/project/berryboot/berryboot-20170527-pi2-pi3.zip) if you have a quadcore RPI.  
   - Download [berryboot-20170527-pi0-pi1-pi2-pi3.zip](http://downloads.sourceforge.net/project/berryboot/berryboot-20170527-pi0-pi1-pi2-pi3.zip) for a singlecore RPI.
2. Unzip the file into an empty fat32 formatted (micro) SD card.
3. Insert the SD card into your RPI and power it up for first boot.
4. You'll be presented with following Berryboot Welcome Screen:
[[https://user-images.githubusercontent.com/8775469/32147239-5a3d5218-bce4-11e7-9947-c54a0e8d1357.png]]   
In this first screen you can enable or disable overscan, check your network connection, set your time-zone and keyboard layout.If your Pi is connected to the Internet BerryBoot will try to detect your location based on your IP-address, and set the right timezone automatically. Verify that it is correct and press “ok”
5. In the next screen you choose were to install:  
[[https://user-images.githubusercontent.com/8775469/32147241-6218820a-bce4-11e7-9d74-26066dff5424.png]]   
Select where you want to store the operating system files, and press “format”
You can choose to install the operating system files: 
- on the SD card itself
- on an external USB stick/disk.
- on networked storage (for more information see: storing your files on a Synology NAS)
Be aware that if you choose an external drive, the files of the operating system will be stored there, but you still need to keep the SD card in the Pi to boot from.

**WARNING: all existing files on the disk will be erased.**

When done you'll be presented with OS installation selection screen, just click cancel, returning to the main Berryboot menu and click exit to reboot your RPI, after which we can proceed to 

## Part 2 Import the NextCloudPi.img into the Berryboot menu
[[https://user-images.githubusercontent.com/8775469/32148601-d812147a-bcf9-11e7-96f7-f33faed236f2.jpg]]
Importing a squashfs image can be done through:
- downloading from network location
- copying from usb

Boot your RPI with Berryboot sd-card and exernal drive used in Part 1.
Put your SquashFS formatted image on a USB stick, go to the “Operating system installer”, **hold down** your mouse button over **“Add OS”** and select “Install from USB stick” 

If you don't have a NextCloudPi squashfs image yet, you can [download latest image or torrent here](https://ownyourbits.com/downloads/)  
Once installed and available in the menu hit exit to reboot and wait for NCP to start. 
There will be short delay before being greeted by Berryboot Menu, and another 10sec delay, in which you can interupt booting and hit the edit menu button to add another or clone/copy your OS in the menu editor. If not just wait 10sec or hit the boot button. If you see the NCP logo, you are ready to [Start using](https://github.com/nextcloud/nextcloudpi/wiki/How-to-access-NextCloudPi) and personalise your own NextCloudPi instance.
[[https://user-images.githubusercontent.com/8775469/32148896-276b15b4-bcfd-11e7-84b9-a1eba36f7e6e.jpg]]

If you have your own custom image, and need to convert it to squashfs, this will be the object of another how to. In the mean time use the instructions through link below.

See also

[How to convert Rasbianfs to squashfs](http://www.berryterminal.com/doku.php/berryboot/adding_custom_distributions)  
[Main Berryboot page](http://www.berryterminal.com/doku.php/berryboot)  

Tweaks
- If your image prefers to have a certain memory split use the extension .img128 .img192, .img224 or .img240 instead of .img.
- If the image you are converting is based on Debian/Raspbian delete the etc/console-setup/cached_UTF-8_del.kmap.gz file before converting the image to force regeneration of the cached keyboard mapping on first boot. This is to make sure it uses the keyboard layout set in Berryboot instead of default British.
