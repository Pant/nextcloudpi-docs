How to get certificate with Letsencrypt using DNS to verify domain.md
=====================================================================

Sometimes ports 80 and 443 are not available.  We are going to use Letsencrypt's certbot `--manual` and `--preffered-challenges dns` options to get certificates and activate them manually. 
You'll need a domain and access to the DNS records to create a TXT record pointing to: _acme-challenge.yourNCP.yourdomain.tld with a challenge value provided by `certbot` when running it with the `dns` option.


1. `sudo apt install certbot python-certbot-apache`
This installs Letsencrypt's certbot and apache module (apache not tested yet)
1. `sudo nano /etc/hosts`
Add a line with your local IP hostname.domain.tld
1. `sudo certbot -d yourNCP.domain.tld --manual --preferred-challenges dns certonly`
This, interactively, generates all the required files and the certificate after providing challenge value for DNS TXT record and succesfully reading the DNS record.
1. `sudo nano /etc/apache2/sites-enabled/nextcloud.conf`
Edit to look like this, certbot provides these locations 
SSLCertificateFile      /etc/letsencrypt/live/yourNCP.domain.tld/fullchain.pem
SSLCertificateKeyFile	/etc/letsencrypt/keys/0000_key-certbot.pem
1. `sudo nano /var/www/nextcloud/config/config.php`
Edit config.php trusted_domains array by replacing the localhost in 0 => 'localhost' with yourNCP.domain.tld:port 
1. `sudo service php7.0-fpm restart`
To restart php7.0-fpm
1. `sudo service apache2 restart`
To restart apache2

You should now be able to access your NCP at https://yourNCP.domain.tld:portnr

I have my test NCP running on port 2443external/443internal, so I have a NAT/port forward accordingly. You are free to access your NCP on any port, now that domain and certificate are verified and installed.