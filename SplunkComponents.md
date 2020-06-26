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
note: you must use httpS in order to be redirected to the login prompt

![To Hit the Webpage](/splunk/SplunkLogin1.png)

You will be prompted by your browser for a user login. Please contact #security-stack on the Slack channel to get credentials
![To Hit the Webpage](/splunk/SplunkLogin3.png)

#### LetsEncrypt

Config files get generated in /etc/letsencrypt/live/splunk.codeforsanjose.com/

``` sudo git clone https://github.com/letsencrypt/letsencrypt /opt/letsencrypt

``` cd /opt/letsencrypt/

``` ./letsencrypt-auto certonly --standalone

*** TO RENEW ***

sudo service nginx stop
 ./certbot-auto renew

root@splunk2:/opt/letsencrypt# ./letsencrypt-auto renew

ubuntu@ip-172-31-19-21:/opt/letsencrypt$ ./letsencrypt-auto certonly --standalone
