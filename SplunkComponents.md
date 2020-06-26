Splunk is a log file aggregator designed to monitor logfiles forwarded from hosts. 
Currently, Code For San Jose supports three live applications, Meal Tally, Open Disclosure, and Disaster Response 
with funding from Code For America.

# COMPONENTS
+ Splunk: Download from Site
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
