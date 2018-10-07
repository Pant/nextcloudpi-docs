How to access outside of your network
=====================================

[nc-forward-ports]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#nc-forward-ports
[freeDNS]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#freeDNS
[no-ip]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#no-ip
[letsencrypt]: https://github.com/nextcloud/nextcloudpi/wiki/Configuration-Reference#letsencrypt

You can do these steps from the TUI or from the WebUI.

#### Port Forwarding
Most home Routers come with a firewall installed which blocks outside requests to inside computers. In order for you to access your Nextcloud from the outside of your house, you need to allow ports 80 and 443 and forward them to your NextCloudP.

The port forwarding can be set up in your routers configuration interface, or, with NextCloudP's Universal Plug-and-Play (UPnP) client [`nc-forward-ports`][nc-forward-ports] which does just that in an easy way.

Note: *You need UPnP to be temporarily enabled in your routers configuration. It is recommended that you disable it again after you've run the command.*

1. Navigate to [`nc-forward-ports`][nc-forward-ports] in the TUI or the WebUI.
2. Set the ports your Nextcloud runs on. (It is recomended that you use the defaults)

#### DDNS
In order to access Nextcloud from outside of your house you need a Domain Name (e.x. cloud.com) or a sub-Domain Name (cloud.example.com). Domain Names are names that are pointing to your IP address. But in most cases, home users do not have a static IP address. You probably have a dynamic IP address, which means that changes from time to time. For that reason, in order to keep your (sub)Domain Name always pointing to your IP address, you need a DDNS (Dynamic DNS) service.

NextCloudPi has two different DDNS clients for two different DDNS providers([FreeDNS](http://freedns.afraid.org/), [No-IP](https://www.noip.com)). You have to register an account from their website. There you can create a subdomain for free, or connect a Domain Name you have purchased.

Note: You only need one DDNS service.

Read [this guide](https://github.com/nextcloud/nextcloudpi/wiki/How-to-access-NextCloudPi#using-your-ddns-domain-inside-and-outside-home) if you have problems accessing from inside your home with the DDNS domain URL.

##### FreeDNS (freedns.afraid.org)
Run the TUI (`nextcloud-config`) or use the WebUI.
Log in to freedns.afraid.com and click "Dynamic DNS". Right click on "Direct URL" next to your record. Paste it in a text editor and select only the hash (the characters after the "?").
1. Navigate to [`freeDNS`][freeDNS] in the TUI or the WebUI.
2. Change `ACTIVE` to `yes`
3. Change the `UPDATEHASH` with yours (delete the example and paste with `ctrl+shift+V`)
4. Change `DOMAIN` with your Domain Name you have registered.
5. (Optional) Change the `UPDATEINTERVAL` to the interval time you want the client to update your IP (Dynamic IPs do not change that often so you can leave the default (5mins)).
6. Click Run or Start.

Now try visit your (sub)Domain Name that you have registered with your browser. It should navigate to the Nextcloud instance.

##### No-IP (www.noip.com)
Run the TUI (`nextcloud-config`) or use the WebUI.
1. Navigate to [`no-ip`][no-ip] in the TUI or the WebUI.
2. Change `ACTIVE` to `yes`.
3. Change `USER` with your user name.
4. Change `PASS` with your password.
5. Change `DOMAIN` with your (sub)Domain Name.
6. Change `TIME` with the interval time you want to update the DNS record. Default 30mins.
7. Click Run or Start.

Now try visit your (sub)Domain Name that you have registered with your browser. It should navigate to the Nextcloud instance.

### Automatic signed SSL certificates 
In order to trust a connection to a website and send your user name and password, you need a SSL certificate. The SSL certificate ensures that the communication is encrypted, so everything you send can only be viewed by the server and not someone who impersonates him. By default NextCloudPi provides a self signed SSL certificate in order to encrypt your communication but it is strongly recomended that you use a certificate from a certificate athority. The NextCloudPi can run the Let's Encrypt client which gets a certificate from https://letsencrypt.org for your (sub)Domain Name. NextCloudPi also configures the web server to use it and renews the certificate once a month.

To configure automatic signed SSL certificates (run the TUI (`nextcloud-config`) or use the WebUI):
1. Navigate to [`letsencrypt`][letsencrypt] in the TUI or the WebUI.
2. Change the `DOMAIN` with your (sub)Domain Name.
3. Change the `EMAIL` with your Email address. (It is recomended to use a valid Email address)
4. Click Run or Start.