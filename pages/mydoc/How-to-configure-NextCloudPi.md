How to configure NextCloudPi
============================

## Choose an User Interface
You can configure the NextCloudPi instance from the terminal user interface (TUI) or from the web user interface (WebUI). 
Note: *The backend is the same.* All options can be accessible in either UI.

### TUI

To access the terminal, you need to have ssh enabled on your Raspberry Pi. For more info look [here](https://github.com/nextcloud/nextcloudpi/wiki/How-to-install-NextCloudPi-on-a-Raspberry-Pi#first-steps).

Alternatively, you can plug in a keyboard and HDMI screen to access the terminal.

![](https://camo.githubusercontent.com/4b2c6bbb044a6bd59a01582017fa91ab85e023a5/68747470733a2f2f6f776e796f7572626974732e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031372f30332f6e63702d636f6e662d373030783435362e6a7067)

#### Raspberry Pi
1. Connect keyboard and HDMI screen.
2. Turn on Raspberry Pi with NextCloudPi SD card image.
3. Login with user `pi` and password `raspberry`.
4. (optional) type `sudo raspi-config` and enable SSH in `Interfacing Options".
5. (optional) type `sudo nextcloudpi-config` and use [`nc-wifi`][nc-wifi] to connect to your WLAN.

#### Linux / Mac
1. Open a terminal.
2. Connect to your Raspberry Pi with `ssh`. You can do that using the command `ssh pi@"localIPAdress"`, where "localIPAdress" (without the quotes) is the Pi's local IP address.
3. Enter the password `raspberry`


#### Windows
1. Install Putty from [it's website](http://www.putty.org/)
2. Run Putty and write the IP address of your Raspberry Pi in the "Host Name" box.
3. Select "SSH" from the "Connection type" buttons. The port number should now change to "22".
4. Click "Open" on the bottom right.
5. Enter password `raspberry`

You now have connected to the NextCloudPi Shell. You can run the command `nextcloudpi-config` to open the TUI.

### WebUI
If you want to configure NextCloudPi with the WebUI:
1. Open a web browser.
2. Write in the URL "https://"raspberryPiAddress":4443", where "raspberryPiAddress" (without quotes) should be replaced with your Raspberry Pi's IP Address.
3. There should be an message saying that the address you are visiting is not secure. You should accept the self-signed certificate. You can do this by clicking advanced on the warning page and then clicking to add exception as shown in the image below:
![Accept Signed NCP certificate.](https://user-images.githubusercontent.com/14947634/34748770-10015646-f596-11e7-8f56-4e33cf5c9260.png)
This happens because by default browsers do not recognize self signed certificates. Later you can [get a certificate from Let's Encrypt](https://github.com/nextcloud/nextcloudpi/wiki/How-to-get-certificate-with-Letsencrypt-using-DNS-to-verify-domain) that your browser will recognize.
4. You will be asked for a password. On older installations it is the same one as the `pi` user, so it will be by default user `pi`, password `raspberry`. On newer installations this changed to user `ncp` and password `ownyourbits`. You should change this password after initial configuration using the `nc-passwd` dialog.

After this you should be able to see the Web Panel.

![](https://ownyourbits.com/wp-content/uploads/2017/09/ncp-web-demo.gif)

---

From here you can configure everything that you need. See the [configuration reference](https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference) for an explanation of all the options.

You can follow these [steps to access from outside](https://github.com/nextcloud/nextcloudpi/wiki/How-to-access-from-outside-your-network).

You can follow these [steps to host your data in a USB drive](https://github.com/nextcloud/nextcloudpi/wiki/How-to-configure-an-external-USB-drive-with-NextCloudPi).

You can follow [this tutorial](https://ownyourbits.com/2017/12/30/sync-nextcloud-tasks-calendars-and-contacts-on-your-android-device/) to sync your NextCloudPi Files, Contacts, Tasks and Calendars with your Android phone.
