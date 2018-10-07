How to configure Let's Encrypt with closed ports 80 and 443
===========================================================

_This entry was originally written by @albrechtar [in this github question](https://github.com/nextcloud/nextcloudpi/issues/186#issuecomment-328333387)_

## How to get SSL certs without using Cert Bot (in case you would need to use alternate ports on your instance of NextCloudPi)

You would need to then manually update your SSL certs on your instance of NextCloudPi.

1.  You will need a domain name that allows you to point to other name servers as well as edit the DNS records.  I purchased my own (most free 3rd tier domains would not allow this.  So I recommend you go to namecheap.com and purchase your domain name (they have them for as low as 2.09 for the first year. Then proceed to dynu.com.  Signup and then click the little gear in the top right area it will take you to your control panel(Screen Shot 1).  You will also need to go to namecheap or wherever you get your domain name and add the name servers for Dynu.  They have very easy to follow tutorials and instructions if you are unable to figure this out.
     1a)  Click DDNS services.
     2a)  Click Add
     3a) If you have your own domain use it on the right (ScreenShot2)
     4a)  Enter your public ip address (I used X to block mine you would enter your full ip address), and click save.
     5a)  Just to the right you will see a cup with pencils in it that says DNS records you will want to click this. (ScreeenShot3, ScreenShot4).

2.  Open another tab in your browser and goto zerossl.com(ScreenShot5)
     2a)  On the left side please click Certificates and Tools (ScreenShot6).
     2b)  Click Start under free SSL Certificate wizard and you will see (ScreenShot7).
     2c)  Enter your email address, enter your domain name (yourdomain.com) select DNS Verification and accept the TOS and SA, and click Next (ScreenShot8)
     2d)  You will be asked to include a www. prefix please select yes.
     2e)  You will see that the system generated the CSR (ScreenShot9).
     2f)  Click next and the system will generate the key.(ScreenShot10).
     2g)  You will click the download icon and download both the CSR and the KEY (ScreenShot11).
     2h)  Click next and you will see (ScreenShot12).
     2i)  Now you will need to go back to your Dynu page (remember we left it open and continue to step 3.

3.  Once you are back on your Dynu page you will notice 4 items (node name, type, TTL, and hostname ScreenShot13).  Please follow the below steps:
     3a)  Change type to be TXT -Text
     3b)  Node Name copy and paste your domain TXT Record from your zerossl page.
     3c) Copy and paste the value field from zerossl into the text field on your dynu page(ScreenShot13). (TTL can stay at 90).
     3d)  Repeat step 3c for the other entry (you have two one for www. and one that is just your domain).
    4d) SSH into your pi, and type nslookup -q=TXT XXX", where XXX is one of the records you just pasted into the Node name in step 3b.
     5e) It will only take a minute or two and then when you run that nslookup it will show you that it sees it (I dont recall the exact wording but it was obvious).
     5f) Go back to your openssl and click next. Once it verifies it will issue your account key and your domain crt files.

Once you have these files you have your SSL certificate and you will need to put it in the correct folder on your instance of NextCloudPi.  I am not 100% certain what file to place these into so I will ask @nachoparker to explain that.

I hope this helps, if anyone has any questions please feel free to message here and I will do my best to help. need to then manually update your SSL certs on your instance of NextCloudPi.

1.  You will need a domain name that allows you to point to other name servers as well as edit the DNS records.  I purchased my own (most free 3rd tier domains would not allow this.  So I recommend you go to namecheap.com and purchase your domain name (they have them for as low as 2.09 for the first year. Then proceed to dynu.com.  Signup and then click the little gear in the top right area it will take you to your control panel(Screen Shot 1).  You will also need to go to namecheap or wherever you get your domain name and add the name servers for Dynu.  They have very easy to follow tutorials and instructions if you are unable to figure this out.
     1a)  Click DDNS services.
     2a)  Click Add
     3a) If you have your own domain use it on the right (ScreenShot2)
     4a)  Enter your public ip address (I used X to block mine you would enter your full ip address), and click save.
     5a)  Just to the right you will see a cup with pencils in it that says DNS records you will want to click this. (ScreeenShot3, ScreenShot4).

2.  Open another tab in your browser and goto zerossl.com(ScreenShot5)
     2a)  On the left side please click Certificates and Tools (ScreenShot6).
     2b)  Click Start under free SSL Certificate wizard and you will see (ScreenShot7).
     2c)  Enter your email address, enter your domain name (yourdomain.com) select DNS Verification and accept the TOS and SA, and click Next (ScreenShot8)
     2d)  You will be asked to include a www. prefix please select yes.
     2e)  You will see that the system generated the CSR (ScreenShot9).
     2f)  Click next and the system will generate the key.(ScreenShot10).
     2g)  You will click the download icon and download both the CSR and the KEY (ScreenShot11).
     2h)  Click next and you will see (ScreenShot12).
     2i)  Now you will need to go back to your Dynu page (remember we left it open and continue to step 3.

3.  Once you are back on your Dynu page you will notice 4 items (node name, type, TTL, and hostname ScreenShot13).  Please follow the below steps:
     3a)  Change type to be TXT -Text
     3b)  Node Name copy and paste your domain TXT Record from your zerossl page.
     3c) Copy and paste the value field from zerossl into the text field on your dynu page(ScreenShot13). (TTL can stay at 90).
     3d)  Repeat step 3c for the other entry (you have two one for www. and one that is just your domain).
    4d) SSH into your pi, and type nslookup -q=TXT XXX", where XXX is one of the records you just pasted into the Node name in step 3b.
     5e) It will only take a minute or two and then when you run that nslookup it will show you that it sees it (I dont recall the exact wording but it was obvious).
     5f) Go back to your openssl and click next. Once it verifies it will issue your account key and your domain crt files.

Once you have these files you have your SSL certificate and you will need to put it in the correct folder on your instance of NextCloudPi. This folder is defined in `/etc/apache2/sites-available/nextcloud.conf`

By default they live under `/etc/ssl`

```
...
SSLCertificateFile    /etc/ssl/certs/ssl-cert-snakeoil.pem                                                       
SSLCertificateKeyFile /etc/ssl/private/ssl-cert-snakeoil.key
...
```

## Screenshots
![](https://user-images.githubusercontent.com/19283265/30248880-0bae800a-965a-11e7-8843-fec87e1401a8.png)
![](https://user-images.githubusercontent.com/19283265/30248881-0f6e18ae-965a-11e7-8eda-dcc740c99af3.png)
![](https://user-images.githubusercontent.com/19283265/30248882-0fab0124-965a-11e7-9113-884532167867.png)
![](https://user-images.githubusercontent.com/19283265/30248883-0fb3716a-965a-11e7-858f-4a6c53c261f4.png)
![](https://user-images.githubusercontent.com/19283265/30248885-0fb899a6-965a-11e7-927f-1a52b0930bbd.png)
![](https://user-images.githubusercontent.com/19283265/30248884-0fb8388a-965a-11e7-9764-c7c19ed00d68.png)
![](https://user-images.githubusercontent.com/19283265/30248886-0fb8cb56-965a-11e7-86df-96cd61bb4abd.png)
![](https://user-images.githubusercontent.com/19283265/30248887-0fb98d70-965a-11e7-8753-aa788fd78541.png)
![](https://user-images.githubusercontent.com/19283265/30248888-0fe3dd64-965a-11e7-8999-87b663137fac.png)
![](https://user-images.githubusercontent.com/19283265/30248889-0fe47e72-965a-11e7-933d-e025148611c2.png)
![](https://user-images.githubusercontent.com/19283265/30248890-0fea86a0-965a-11e7-9083-39914a54d327.png)
![](https://user-images.githubusercontent.com/19283265/30248891-0feabc42-965a-11e7-9277-3fff58786c10.png)