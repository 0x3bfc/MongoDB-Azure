# Deploy MongoDB Shard Cluster on Windows Azure

This package is a libaray based on Ansible and Vagrant to deploy and manage a mongoDB shard cluster 
on Windows Azure. It installs and configures MMS (MongoDB Management System) over MongoDB
Cloud also it uses NewRelic (A software analytics tool suite) to monitor MongoDB cluster servers
and the running services on your cluster. The following steps describe how to manage monogDB 
services (Mongod, Mongos and mongoc), automate backup/restore over cloud, monitor mongo services
and monitor all running services in your infrastructure to make sure that it satisfies the availability and 
consistency of Mongo database.


# Basic Cluster Architecture

TBA

# Install Vagrant

TBA

# Install Windows Azure CLI

 1. Ubuntu 12.04 LTS Precise Pangolin:
	
        $ sudo apt-get install curl
        $ curl -sL https://deb.nodesource.com/setup | sudo bash -
        $ sudo apt-get install -y nodejs
        $ sudo npm install -g azure-cli


 2. Ubuntu 14.04 LTS Trusty Tahr: 

        $ sudo apt-get install nodejs-legacy
        $ sudo apt-get install npm
        $ sudo npm install -g azure-cli

# Create and manage Azure's certificates

TBA

# Configure your Vagrant File

TBA

# NewRelic Server Monitor

Here I introduce how to get your NewRelic license key to port it into your ansible, to keep 
your servers monitored

        1- login to windows azure portal
        2- select Marketplace ---> from popup select NewRelic app service
        3- once NewRelic Service is up, from NewRelic dashboard in windows azure click on Manage "at the bottom of page"
        4- from NewRelic account select servers from the tap on the top of page.
        5- choose your platform by clicking on 'RedHat Enterprise Linux 5+, Centos 5+'.
        6- scrol down to the end of the page and copy your license key as show below.
                    license_key=55bbd90f482XXXXXXXXXXXXXXXXXXXXXXX_
        7- add this license key in this file mongo-azure/roles/newrelic/defaults/main.yml

# MongoDB Management Service (MMS)


        1- create New MMS free account from mms portal https://mms.mongodb.com/
        2- Once you login to your account click on Begin setup button.
        3- select Manage Existing to manage your MongoDB on Azure.
        4- click on install agent and select RHEL/Centos(5.x,6.x)/SUSE/Amazon
        5- From the pop-up screen get the following two arguments
	
			mmsGroupId=558a6XXXXXXXXXXXXXXXXXXXXX
			mmsApiKey=eeb066XXXXXXXXXXXXXXXXXXXXX
	
        add these values in this file: mongo-azure/roles/mms/files/automation-agent.config.j2 


# Start MongoDB Deployment

finally start mongodb-full deployment by using the following command line:
	
	ansible-playbook -i hosts playbook.yml -vvvv


Your cluster is ready check your NewRelic and MMS services



To access your mongos router from master node:

	/usr/bin/mongo master:8880/admin -u admin  -p ADMINPASSWORD

# Backup/Restore management using MMS

TBA
