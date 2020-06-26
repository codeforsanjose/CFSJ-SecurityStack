Splunk is a log file aggregator designed to monitor logfiles forwarded from hosts. 

This page is for a more in depth overview on the technical details for setup

The following can be modified to fit with any implementation of Splunk CE

# COMPONENTS
+ Splunk CE: Download from Site
+ LetsEncrypt: For HTTPS encryption
+ Nginx: Reverse Proxy for Login
+ Firewall Rules (AWS): Restrict access to App

Splunk Community Edition does not have login features or users. However the workaround is to use Nginx Reverse Proxies and .htaccess. 

https://splunk.codeforsanjose.com

## LetsEncrypt

Config files get generated in /etc/letsencrypt/live/splunk.codeforsanjose.com/

` sudo git clone https://github.com/letsencrypt/letsencrypt /opt/letsencrypt`

` cd /opt/letsencrypt/ `

` ./letsencrypt-auto certonly --standalone `

**TO RENEW**

` sudo service nginx stop`
` ./certbot-auto renew `

` /opt/letsencrypt$ ./letsencrypt-auto renew`

` /opt/letsencrypt$ ./letsencrypt-auto certonly --standalone`

## Splunk Config
Moved letsencrypt files to splunk directory

** "/opt/splunk/etc/system/local/web.conf" ** 
```[settings]
enableSplunkWebSSL = 1
privKeyPath = /opt/splunk/etc/auth/splunk.codeforsanjose.com/privkey.pem
caCertPath = /opt/splunk/etc/auth/splunk.codeforsanjose.com/fullchain.pem
root_endpoint=/ ```


** "/opt/splunk/etc/system/local/server.conf" **
``` ....
[proxyConfig]
http_proxy = http://splunk.codeforsanjose.com:80
https_proxy = https://splunk.codeforsanjose.com:443 .... ```


## Nginx 

**/etc/nginx/conf.d/loginapp.conf**

MAKE SURE YOU SPECIFY PROXY PASS CORRECTLY
	
``` server{

        listen 443 ssl;
        listen [::]:443 ssl;
        server_name splunk.codeforsanjose.com www.splunk.codeforsanjose.com;

        ssl_certificate /etc/letsencrypt/live/DIRECTORY/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/DIRECTORY/privkey.pem;

        ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3;

        ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
        ssl_prefer_server_ciphers on;
        ssl_stapling on;
        ssl_stapling_verify on;
        #return 301 http://$host$request_uri;
        auth_basic_user_file <LOCATION OF .ht FILE>
        auth_basic "Splunk App";
        location / {
                auth_basic "Splunk App";
                proxy_pass https://splunk.codeforsanjose.com:8000;
                auth_basic_user_file <LOCATION OF .ht FILE>;
        }
````}
`


## Firewall Rules

There are various ways to do this but primarily you only want the ip address itself to be able to access the application 
For Non-AWS instances, use IPTables
For AWS, you can edit the inbound rules as follows

HTTP	TCP	80	0.0.0.0/0	Allow for Web Traffic

Custom TCP	TCP	8000	54.241.132.254/32	Allow for Splunk Console access

HTTPS	TCP	443	0.0.0.0/0	Allow for SSL Web Traffic

Set it to only allow port 8000 traffic from itself, remember we're working with a reverse proxy


![FW](/splunk/Splunk-aws-fw-rules.png)
`
