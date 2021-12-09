# Lab 4: Manage Packages and Services on a Linux VM (Azure or AWS)

1. Create a Linux VM
2. Install the Apache Web Server
3. Start the service status via command line
4. Investigate the service status via command line
5. Stop the service 

Challenge: Create a boostrapping script that will install and start this service on new EC2 VMs

### Notes:

Install and Configure Apache (Ubuntu)
* https://ubuntu.com/tutorials/install-and-configure-apache#1-overview

How to install Apache on RHEL 8 / CentOS 8 Linux
* https://linuxconfig.org/installing-apache-on-linux-redhat-8

How to use cloud-init to customize a Linux virtual machine in Azure on first boot
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-automate-vm-deployment

Create bootstrap actions to install additional software
* https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-bootstrap.html

# Notes From My LAB 4 Experience 


## 1. Create a Linux VM
I was able to create a linux Virtual machine using AWS platform. I created the Instance using CLI, configured the images and region and I ssh into the running instance. full details on this was explicitly explained in the previouis labs (1, 2, 3)

## 2. Install the Apache Web Server
One can install a web server on a running instance. I was able to install a web server (apache) into my running virtual machine using the CLI, I was able to run the following command

 *yum update -y* \
 
  *yum install -y httpd* \
  
  ( this is the command to install apache web server).

## 3. Start the service status via command line
After installing any server on instances or even installing applications on our local system we need to start the application for it to function. Same goes for the web server installed on our various instances we need to start the web server for it to run so we use the following command given that apache is already installed successfully on the instance.

*sudo systemctl start httpd*

(If this is succeful it means we have started the installed web sever on our instance) of which after i did run the command, it was succesful

## 4. Investigate the service status via command line
After i've successfully installed and started our web server, I need to check it's status to confirm whether or not it is running. We can do this by actually viewing the server using our IP address.

### Note
That port 80 will have to be opened in order  to be able to view the server in action usisng our IP address.

Using the CLi we can view the status of our installed web server which is apache by running the following command

*sudo service httpd status*

 (this is to check whether or not the web server which is apache is running)

## 5. Stop the service.
The following command is to disable or stop the apache service from running

*sudo systemctl disable httpd*

(this is to disable apache from running on our instance)

*sudo systemctl stop http*

(this is to stop apache from running on our instance).