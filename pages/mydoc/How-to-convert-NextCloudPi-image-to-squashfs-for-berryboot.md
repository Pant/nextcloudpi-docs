How to convert NextCloudPi image to squashfs for berryboot
==========================================================

Adding your own custom operating systems to the Berrboot menu

You can add your own extra operating systems to the Berryboot menu. However this requires that you convert your file system image to SquashFS format first.

Most Raspberry Pi operating system images are disk images containing two partitions. A FAT partition with the boot loader and kernel files, and a second ext4 partition with everything else. We are interested in the second partition.

With a regular Linux desktop computer that has kpartx and mksquashfs installed, you can convert the second partition to SquashFS like this:

`$ tar xfv NextCloudPi_12-04-17.tar.bz2`

`$ sudo kpartx -av image_you_want_to_convert.img `

> add map loop0p1 (252:5): 0 117187 linear /dev/loop0 1

> add map loop0p2 (252:6): 0 3493888 linear /dev/loop0 118784

`$ sudo mount /dev/mapper/loop0p2 /mnt`

`$ sudo sed -i 's/^\/dev\/mmcblk/#\0/g' /mnt/etc/fstab`

or 

`$ sudo nano /mnt/etc/fstab` 

comment out each lines with a ‘#’ 

uncomment /boot in fstab and let it point to LABEL=boot  or /dev/mmcblk0p1

`$ sudo rm  /mnt/etc/console-setup/cached_UTF-8_del.kmap.gz`

`$ sudo mksquashfs /mnt converted_image_for_berryboot.img -comp lzo -e lib/modules`

`$ sudo umount /mnt`

`$ sudo kpartx -d image_you_want_to_convert.img `


Notes: 

If kpartx reports it created a mapping different than loop0p2 (e.g. loop4p2) mount that instead. This can happen if loop0 is already in use by something else on the system.
We are excluding /lib/modules from the image, because the kernel modules shipped with Berryboot are used instead, and shared with all distributions.

Some older versions of mksquashfs do not support the ”-comp lzo” option. You can leave it out to let it use gzip compression instead. Advantage of LZO is that it is faster to uncompress, which is a big plus on slow ARM devices, and therefore preferred. This does come at a cost of reduced compression ratio (LZO images are larger than gzip ones).

Put your SquashFS formatted image on a USB stick, go to the “Operating system installer”, hold down your mouse button over “Add OS” and select “Install from USB stick” If your image prefers to have a certain memory split use the extension .img128 .img192, .img224 or .img240 instead of .img.
Tweaks

If the image you are converting is based on Debian/Raspbian delete the etc/console-setup/cached_UTF-8_del.kmap.gz file before converting the image to force regeneration of the cached keyboard mapping on first boot. This is to make 
sure it uses the keyboard layout set in Berryboot instead of default British.
