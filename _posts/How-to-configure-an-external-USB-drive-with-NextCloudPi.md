How to configure an external USB drive with NextCloudPi
=======================================================

[nc-automount]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#nc-automount
[nc-format-USB]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#nc-format-usb
[nc-datadir]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#nc-datadir
[nc-database]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#nc-database
[nc-swapfile]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#nc-swapfile

This guide will help you configure an external USB drive.

**Important note:** If you are using only one USB drive, you can leave the default path `/media/USBdrive` for all configuration options, but if you are going to use more than one you need to reference them by _label_, or NCP will not be able to know which one is which. For instance, if the label of the drive is _mylabel_ then use the path `/media/mylabel` for items such as `nc-datadir`, `nc-database` and so on.

# Procedure
1. Format USB drive (optional but check note).
2. Enable [`nc-automount`][nc-automount].
3. Configure Nextcloud data to be on the USB drive.
4. Configure Database data to be on the USB drive (optional).
5. Configure Swap on the USB drive (optional).

# Format USB drive (optional)

[`nc-format-USB`][nc-format-USB] will format your external USB drive to EXT4, with the given Label. 

_**Note 1:**_  _In order for you to be able to use an external USB drive, the USB drive must not be formatted as NTFS/FAT as these do not support the user/permission system._

_**Note 2:**_  _This will format all USB drives you have connected to the Raspberry Pi_

1. Navigate to [`nc-format-USB`][nc-format-USB] in the TUI or the WebUI.
2. Change the LABEL to a label you like. This is also the name of the directory that the USB drive will mount to (e.x. /media/"myLabel").
3. Click Run or Start.

# Enable [`nc-automount`][nc-automount]

To enable [`nc-automount`][nc-automount] follow the steps:

1. Navigate to [`nc-automount`][nc-automount] in the TUI or the WebUI.
2. Change `ACTIVE` to yes.
3. Click Run or Start.

# Configure Nextcloud data to be on the USB drive

To make Nextcloud data directory to be on the USB drive, follow the steps:

1. Navigate to [`nc-datadir`][nc-datadir] in the TUI or the WebUI.
2. Change `DATADIR` to your data location in the mount point.
3. Click Run or Start.

# Configure Database data to be on the USB drive (optional).

To make Database data to be on the USB Drive, follow the steps:

1. Navigate to [`nc-database`][nc-database] in the TUI or the WebUI.
2. Change `DBDIR` to your database location in the mount point.
3. Click Run or Start.

# Configure Swap on the USB drive (optional).

To configure Swap location and size, follow the steps:

1. Navigate to [`nc-swapfile`][nc-swapfile] in the TUI or the WebUI.
2. Change the `SWAPFILE` to the desired location in the mount point.
3. Change the `SWAPSIZE` to the desired size of Swap File (Default: `1024MB`).

# Final Words

Now you have configured NextCloudPi to use an external USB drive for Nextcloud data, optionally Database data and Swap.
