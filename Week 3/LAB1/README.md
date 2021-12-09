# Lab 1: Install a LAMP stack on an Azure Linux VM

1. Create a resource group
2. Create a virtual machine
3. Open port 80 for web traffic
4. SSH into your VM
5. Install Apache, MySQL, and PHP
6. Install WordPress

### Notes:

Tutorial: Install a LAMP stack on an Azure Linux VM
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-lamp-stack

Sample Gist
* https://gist.github.com/mikepfeiffer/96d659042f0575a617648a33c92b8f4a

Build and run a web application with the MEAN stack on an Azure Linux virtual machine
* https://docs.microsoft.com/en-us/learn/modules/build-a-web-app-with-mean-on-a-linux-vm/

MEAN Stack App
* https://github.com/MicrosoftDocs/mslearn-build-a-web-app-with-mean-on-a-linux-vm

# Notes From my LAB 1 Experience 

## 1. Create a resource group
I created a resource group on my Azure account using the cloud shell which i am now conversant with. 

I used bash on the cloudshell to create my resource group. I used this command to create the resource group;

a*z group create* \

*--name myresourcegroup2* \

*--location eastus2*

## 2. Create a virtual machine
Just like creating a resoucre group, I am now conversant with creating a VM  both on the GUI and using the Cloud Shell

I was able to create a VM with the following commands;

*az vm create --resource-group myresourcegroup2* \

*--name mysecondvm* \

*--image UbuntuLTS* \

*--admin-username lanreazure* \

*--generate-ssh-keys* 

Meaning i created a resource group (myresourcegroup2), named it (mysecondvm), UbuntuLTS was my prefered OS template and I generated ssh-key which i will use to ssh into the vm 

## 3. Open port 80 for web traffic
Again opening inbound rules and outbound are now things I do confidentally do on CLI and GUI, I can now open different port for diferent uses, port 80, port 22,port 443... just like port 22 is for ssh, port 80 is for web traffic and the Virual machine i am creating WILL BE USED AS A WEB SERVER  so i opened port 80 on cloushell using this command

*az vm open-port --port 80 --resource-group myresourcegroup2 --name mysecondvm*

## 4. SSH into your VM
over time, I have been able to learn how to SSH into my VM. Although, at first i was alway had an error message [Permission Denied(public key)] but i havee identified why i always had that error message and now I am able to ssh into my Vm's without stress. 

I ssh into my Vm to install a LAMP stack (Linux, Apache, Mysql, PHP).

## 5. Install Apache, MySQL, and PHP
To install the LAMP stack (Linux, Apache, Mysql, PhP), I was able to learn and run the commands to install the various applications from how we were taught during the bootcamp lecture

Although they can be installed easily using the GUI,I was able to install mine using various commands taught during the lecture. I was able to install Apache, PHP and Mysql using this command on Azure portal.

*sudo apt update && sudo apt install lamp-server^ -y* 

(-y command is the automatic yes I want to install without query)

I was able to verify my apache using the command (*apache2 -v*)

 I was able to verify and secure mysql installation using the command  *(sudo apt update && sudo apt install lamp-server^ -y)* 
 
  I was able to validate my login, created a PHP page on my VM.

## 6. Install WordPress
Just like the LAMP stack I installed wordpress using the following command

*sudo apt install wordpress -y* 

(just as always, -y means yes install for me without querry). 

*sudo nano wordpress.sql*

using this commnand i was able to write a wordpress script
I was able to view all my applications in action and also edited my wordpress content.