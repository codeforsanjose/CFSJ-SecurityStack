Splunk is a log file aggregator designed to monitor logfiles forwarded from hosts. 

This page is for a more in depth overview on the technical details for setup

The following can be modified to fit with any implementation of Splunk CE

# COMPONENTS
+ Splunk CE: Download from Site
+ LetsEncrypt: For HTTPS encryption
+ Nginx: Reverse Proxy for Login
+ Firewall Rules (AWS): Restrict access to App

Splunk Community Edition does not have login features or users. However the workaround is to use Nginx Reverse Proxies and .htaccess. 

#### To access:
https://splunk.codeforsanjose.com

#### LetsEncrypt

Config files get generated in /etc/letsencrypt/live/splunk.codeforsanjose.com/

` sudo git clone https://github.com/letsencrypt/letsencrypt /opt/letsencrypt

` cd /opt/letsencrypt/

` ./letsencrypt-auto certonly --standalone

*** TO RENEW ***

` sudo service nginx stop
` ./certbot-auto renew

` /opt/letsencrypt$ ./letsencrypt-auto renew

` /opt/letsencrypt$ ./letsencrypt-auto certonly --standalone
