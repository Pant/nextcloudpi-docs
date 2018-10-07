How to access NextCloudPi
=========================

[nc-wifi]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#nc-wifi

This guide will help you access NextCloudPi.

# Access

## Instant Domain Name Access
When up and running, your device should become accessible at [https://nextcloudpi](https://nextcloudpi) or [https://nextcloudpi.local](https://nextcloudpi.local).

![](https://ownyourbits.com/wp-content/uploads/2017/09/local-access1.jpg)

If you are using Windows you may have to install [Bonjour Services for Windows](https://support.apple.com/kb/DL999)  to make it discover the .local domains. If your Browser redirects you to some search engine, you may try pasting the whole adress (including https://) at once.

If this does not work, try the following to discover your Pi's IP address directly.

## Find the IP address of the Raspberry Pi
You need to find the local IP address of the Raspberry Pi in order to connect to it and configure it.

### From the screen
If you connect a monitor with a HDMI cable to your Raspberry Pi, you will see the local IP address.

![screen-ip](https://ownyourbits.com/wp-content/uploads/2017/02/nextcloudpi_boot.jpg)

### From your home Router Web Interface
Note: *Routers do not share the same Web User Interface.*  
1. Open a Web Browser, like Firefox.
2. Visit your home Router IP address. It is written at the bottom of your Router. Normally it will be 192.168.1.1
3. Log in with your credentials
4. Navigate to an entry in your menu that shows your Network Map and find a list that shows the IPs of the connected devices. The Raspberry Pi's IP address should be listed there.

### Linux / Mac
1. Install `nmap` from your package manager.
2. Open a terminal 
3. Run the command `nmap -sP '192.168.0.*'`, where you have to replace the network IP (192.168.0) with yours.
You will see something like this:
```
Nmap scan report for 192.168.0.131 (192.168.0.131)
Host is up (0.016s latency).
MAC Address: AA:BB:CC:11:22:33 (Raspberry Pi Foundation)
```

The local IP address of this Raspberry Pi is `192.168.0.131`

### Windows
1. Install `Angry IP Scanner` from [it's website](http://angryip.org/).
2. Run `Angry IP Scanner` and put your network range and netmask. For example `From: 192.168.0.0` `To: 192.168.0.255` `Netmask: /24`.
3. Hit start.

You will get a list of all connected devices on your network. For more info look at the [FAQ](http://angryip.org/faq/) of Angry IP Scanner.

## Access from outside home network

See [this guide](https://github.com/nextcloud/nextcloudpi/wiki/How-to-access-from-outside-your-network)

## Using your DDNS domain also inside NextCloudP's home network

Most probably, you will want to use the same DDNS domain inside your house that you setup to use [from outside](https://github.com/nextcloud/nextcloudpi/wiki/How-to-access-from-outside-your-network).

That way, your phone, tablet and laptop can seamlessly access your cloud regardless where you are.

First, just try to access NCP using your working DDNS domain, for instance _mycloud.freeDNS.org_

If it works your're all set, otherwise your router doesn't support automatic _NAT loopback_, and you should try

* A) to configure an additional address entry for your domain (that points to the local NextCloudP IP) in the DNS server or forwarder of your router. (For example, if the router uses dnsmasq and the IP is as in the example above: `address=/your.ddns.domain/192.168.0.131`)

If that is not possible, you may enable and use a DNS server on NextCloudP.

* B1) Enable the [dnsmasq](https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#dnsmasq) in the NextCloudPi configuration. Just enter your registered DDNS domain as DOMAIN, and the IP of your router (as DNSSERVER).

* B2) Let your computers and devices use NextCloudP's DNS server when connected inside your house:

  * 2.1) Preferably, your router allows to announce a configurable DNS Server to your devices in its DHCP configuration,

  * 2.2) Otherwise, you will have to configure the NextCloudP's IP as primary and secondary DNS server for your local network connection (usually in the network manager). For more in depth information on this see [this post](https://ownyourbits.com/2017/03/09/dnsmasq-as-dns-cache-server-for-nextcloudpi-and-raspbian/)

---

# Activation

Now, we can start using NextCloudPi! first type the IP address or domain in your browser, then we have to activate NCP.

We will be presented with an activation page. Print the page or copy the passwords, and hit 'Activate'. We can change these passwords later with `nc-admin` and `nc-passwd`.

![](https://ownyourbits.com/wp-content/uploads/2018/04/ncp-activation.gif)

We will be redirected to ncp-web where we can run the first run Wizard.

![](https://ownyourbits.com/wp-content/uploads/2017/10/wizard-demo1.gif)

From this point we can access Nextcloud by the IP address, nextcloudpi.local or the DDNS domain name we have registered. We can access the web panel at port 4443, for example https://nextcloudpi.local:4443

Next, learn [how to configure NextCloudPi](https://github.com/nextcloud/nextcloudpi/wiki/How-to-configure-NextCloudPi).