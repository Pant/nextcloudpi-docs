How to install NextCloudPi
==========================

[ssh]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#ssh

## Download the Image for your Hardware

If you are comfortable using BitTorrent please use it for downloading and share the Torrent files to save us some server traffic, thank you! For this you can use a BitTorrent client like [Transmission](https://transmissionbt.com/download/) and leave it running to continue serving the files after downloading.

You'll find the torrent, as well as a magnet links to and the direct downloads of the NextCloudPi system images at [nextcloudpi.com](https://ownyourbits.com/nextcloudpi/#download). Click the download icon and you'll see a list of folders that contain the links and .tar.bz files. 


## MD5 checksum (to verify the download)
Can be generated in Windows using the Command Prompt & the command

    certutil -hashfile  <path to the file>\<filename> MD5

Linux (from shell)

    md5sum <path to the file>\<filename>

## Installing

You can run NextCloudPi from an SD card or from a USB drive.

### Option 1: Run from SD card

If your computer has a slot for SD cards, insert the card. If not, insert the card into an SD card reader, then connect the reader to your computer.

#### Linux & Mac
1. Open a terminal and run the following commands.
2. Replace "user" with your user name and run command `cd /home/user/Downloads` (or any other folder you've saved the files to).
3. Check the file for corruption (optional). Run the command `md5sum NextCloudPi_XX-XX-XX.tar.bz2` and compare it with the hash in file `md5sum`, which you can find in downloads page.
4. Replace XX-XX-XX with the version you downloaded and run the command `tar -xvf NextCloudPi_XX-XX-XX.tar.bz2` to extract the image.
5. Run command `sudo dd bs=4M if=NextCloudPi_XX-XX-XX.img of=/dev/sdx`, where `/dev/sdx` is your sd card name. (For more info look [here](https://www.raspberrypi.org/documentation/installation/installing-images/linux.md))
6. Run command `sync`.

#### Windows
1. Install Etcher from [their website](https://etcher.io/)
2. Install 7-Zip from [their website](http://www.7-zip.org/)
3. Run 7-Zip manager, find your downloaded .tar.bz2 file, right click and choose "extract here". Next select the .tar file you just extracted, right click and choose "extract here" again. You should now see an .img file.
4. Run Etcher and click "Select Image". Find your image (the .img file) you have just extracted and click "Open".
5. Etcher automatically detects the SD card, but verify that is the one you want the image to be installed on.
6. Click "Flash" in Etcher.


### Option 2: Hybrid (/boot partition on SD card, / partition on USB)

This will limit the media errors that usually happen when running from SD card, but will result in spinning up a USB harddisk more often. After the Option 1 steps you can [move the root partition to HD or SSD](https://elinux.org/Transfer_system_disk_from_SD_card_to_hard_disk). On Armbian based images you may install a tool to do this: `apt install armbian-config`.


### Option 3: Run from USB drive

Warning, this will permanently set the Raspberry Pi to only boot from USB. If you want this, follow [these steps](https://www.raspberrypi.org/documentation/hardware/raspberrypi/bootmodes/msd.md)

NOTE: help needed to further explain the required steps in this section. If you are taking this path, please consider editing this wiki.

### Option 4: Install NextCloudPi on SD or external usb drive with Berryboot 
[Wiki/HowTo here](https://github.com/nextcloud/nextcloudpi/wiki/How-to-install-NextCloudPi-on-an-external-drive-using-Berryboot.)

## First steps

### Enable SSH (optional)

Secure shell (SSH) provides a powerful command line based text interface to configure NextCloudPi for experts, and is not needed to just use NextCloudPi.

#### Before the first run

If you need secure shell access on the first boot, in order to connect to your Raspberry Pi, create a file named `ssh` (without any extension) at the boot partition of your SD card. (More info [here](https://www.raspberrypi.org/documentation/remote-access/ssh/))


#### Once NextCloudPi is running

1. [Navigate to the WebUI or the TUI](https://github.com/nextcloud/nextcloudpi/wiki/How-to-configure-NextCloudPi).
2. Select [`SSH`][ssh] from the list.
3. Change `Enabled` to `yes`.
4. Type in `USER` an existing or a new user that you want to create.
5. Type in `PASS` a password to update the password for an existing user, or to create a password for a new user.
6. Type in `Confirm` your password again.
7. Click Run or Start.

### Run NextCloudPi
Remove the SD card and insert it to the Raspberry Pi. Then connect the Raspberry Pi to your home router with an ethernet cable and power on your Raspberry Pi.

---

Now you have Nextcloud up and running, now setup it up by learning [how to access NextCloudPi](https://github.com/nextcloud/nextcloudpi/wiki/How-to-access-NextCloudPi)