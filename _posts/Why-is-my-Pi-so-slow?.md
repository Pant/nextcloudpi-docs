Why is my Pi so slow?
=====================

# Why?
The RaspberryPi has very limited in IO because micro SD card is slow and the USB-Bus is shared between USB(-Storage) and Ethernet(Network). 
Circa 35 MB/s are shared between USB (the external storage when Nextcloud-data is moved there) and Ethernet.
[rpi-usb-discussion](https://raspberrypi.stackexchange.com/questions/45130/why-do-the-usb-ports-and-ethernet-port-share-the-same-controller). 
Data is pulled from and pushed to RAM, micro-SD-card and if used, USB-Storage.
## Micro SD Card
[RPI3 micro-sd-card speed](https://raspberrypi.stackexchange.com/questions/43618/raspberry-pi-3-micro-sd-card-speed) is slow! Circa 20MB/s.
## USB-Storage
Data must pass Ethernet or WLAN to go to the users.
When external USB storage is used, the data are pulled from USB and pushed on the same BUS back to pass Ethernet-Interface. Ethernet takes 10MB/s of these 35MBs so 25MB/s are left in the same Moment for other USB devices like your external USB-Storage. This is the bottleneck!

On shared media there is also the latency higher when processes are waiting for accessing data.
# What can we do? Or what is best practice?
## How to reduce IO on the USB-BUS?
* We can use WLAN for accessing the device so load is taken away from USB-BUS.
* If Nextcloud-Data and Nextcloud-Database are on the same Storage device (e.g. the USB-Storage) move the Nextcloud-database (back) to another device (e.g. the micro-SD-card). So database-access and file-access are on different devices.
* Use low latency storage e.g. fast micro-sd-cards [Samsung, Sandisk for example](http://www.pidramble.com/wiki/benchmarks/microsd-cards) or SSDs on USB-adapters.
* Not testet but maybe useful is micro sd card bus [overclocking](https://www.jeffgeerling.com/blog/2016/how-overclock-microsd-card-reader-on-raspberry-pi-3).
# RAM
We have 1GB RAM which is nice but not for every Nextcloud-App is this enough to perform well.
## Nextcloud-Apps
* The new Talk-App of Nextcloud 13 is eating a pretty lot of RAM and slows down login. So you should avoid to use Talk on the Raspberrypi if you doesn't want to have a bad user experience.
* Theming-App also slows down login because the Theme must be loaded after defaults are loaded. If you use your own Logo and backgroud this must also be loaded and slows down first Page load before you can login.
* Preview Pictures are generated on demand. This is slow! There is an Nextcloud-App called [Preview-Generator](https://apps.nextcloud.com/apps/previewgenerator) which shifts the on demand load of preview generating to an interval (10 Minutes) based preview generating for new pictures. This speeds opening pictures up because there is no demand to generate a preview but due to IO limitation is loading of picture-previews in the Gallery-App still slow.

**_Please add here other Nextcloud-Apps users should avoid to use or which have a significant performance impact!_**

## Database
By default the database is cached to RAM if it is smaller then 15MB.
This can be increased if database is bigger then 15MB.
Maybe there are other tweaks to speed things up. 