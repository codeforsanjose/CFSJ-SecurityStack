# Security Stack @ Code For San Jose

###### Goals 
###### Getting Started
###### Splunk Components
+ Splunk: Download from Site
+ LetsEncrypt: For HTTPS encryption
+ Nginx: Reverse Proxy for Login
+ Firewall Rules (AWS): Restrict access to App


## Goals

To improve the security stance of projects and give recommendations for deployment

 - Audit existing apps built and partially maintained by Code for San Jose
 - Alerting for security-related events 
 - Provide metrics such as uptime and performance 

## Getting Started

**Splunk Instance: https://splunk.codeforsanjose.com:8000/en-GB**

Request Access: Contact Splunk admin on the # security-stack channel in Slack

Example Queries: 

`index=main` 

Make sure to specify the time range between 2 to 3 hours, this will lighten the load on the server and make sure that we do not exceed the maximum requests


## Splunk Components

**What Is It**

Splunk is basically a log collector. It's where sysadmins and security analysts can correlate system logs from web apps and hosts to identify significant events.

Currently, Code For San Jose supports three live applications, Meal Tally, Open Disclosure, and Disaster Response 
with funding from Code For America.

Splunk Community Edition does not have login features or users. However the workaround is to use Nginx Reverse Proxies and .htaccess. 

#### To access:
https://splunk.codeforsanjose.com
note: you must use httpS in order to be redirected to the login prompt

![To Hit the Webpage](/splunk/SplunkLogin1.png)

You will be prompted by your browser for a user login. Please contact #security-stack on the Slack channel to get credentials
![To Hit the Webpage](/splunk/SplunkLogin3.png)


**For Consumers**

To onboard applications, you can either comment on the # security-stack channel, or you could do the setup yourself. 

**Setup** 

On the host where the web application is running: 


1. `wget -O splunk-8.0.0-1357bef0a7f6-linux-2.6-amd64.deb 'https://www.splunk.com/bin/splunk/DownloadActivityServlet?architecture=x86_64&platform=linux&version=8.0.0&product=splunk&filename=splunk-8.0.0-1357bef0a7f6-linux-2.6-amd64.deb&wget=true'
`
2. `sudo dpkg -i splunk-8.0.0-1357bef0a7f6-linux-2.6-amd64.deb`
3. `cd /opt/splunk/bin`
4. `./splunk add monitor /var/log/`
5. `splunk add forward-server 54.241.132.254:9997`
6. `sudo ./splunk restart`


