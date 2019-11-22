

# Security Stack @ Code For San Jose

## Goals:
 - Audit existing apps built and partially maintained by Code for San Jose
 - Alerting for security-related events 
 - Provide metrics such as uptime and performance 


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

