

# Security Stack @ Code For San Jose

## Goals

To improve the security stance of projects and give recommendations for deployment

 - Audit existing apps built and partially maintained by Code for San Jose
 - Alerting for security-related events 
 - Provide metrics such as uptime and performance 

## Getting Started

**Splunk Instance: https://splunk.codeforsanjose.com:8000/en-GB**

Request Access: Contact Splunk admin on the # security-stack channel in Slack
A temporary passcode will be sent to your email. 

Example Queries: 

`index=main` 

Make sure to specify the time range between 4 to 6 hours, this will lighten the load on the server and make sure that we do not exceed the maximum requests

## Components
### Splunk

Onboard hosts and connect them up to the main host

wget -O splunk-8.0.0-1357bef0a7f6-linux-2.6-amd64.deb 'https://www.splunk.com/bin/splunk/DownloadActivityServlet?architecture=x86_64&platform=linux&version=8.0.0&product=splunk&filename=splunk-8.0.0-1357bef0a7f6-linux-2.6-amd64.deb&wget=true'

sudo dpkg -i splunk-8.0.0-1357bef0a7f6-linux-2.6-amd64.deb

cd /opt/splunk/bin 

sudo ./splunk start


### Saltstack

Config control, automatic updates 


### Terraform

Deploy from Digital Ocean Droplets

