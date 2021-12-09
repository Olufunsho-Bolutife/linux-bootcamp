# Lab 1: Create a Linux virtual machine with the Azure CLI

1. Launch Azure Cloud Shell
2. Create a resource group
3. Create virtual machine
4. Open port 80 for web traffic
5. Connect to virtual machine
6. Install web server
7. View the web server in action

### Notes:

Quickstart: Create a Linux VM
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-cli

Quickstart for Bash in Azure Cloud Shell
* https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart

# Notes on my LAB 1 Experience 
## 1. Launch an Azure Cloud shell
The very first thing to do is go to the Azure portal. Please note that you must have created an Azure account first before you can access the Azure portal. When you arrive at the portal go to the notification bars and click on the first box from your left. Clicking on that will launch the Azure Cloud shell.
## 2. Create a resource group
A Resource Group is a tool(a group that is saved on the portal) that holds every created resources for an Azure service
An azure resource group can be seen as a folder which is used to group related, interdependent or logically linked Azure resources together.

When creating an Azure Resource Group, you need to specify the following:

#### 1. The region you want the Resource Group to be located.
#### 2. The name of the Resource Group that is being created.

 to create a simple resource group within a specified location I simply ran this command

*az group create --name MyResourceGroup1 --locattion eastus*

## 3. Create virtual machine

An Azure Virtual Machine can be created using either Azure Portal or the cloud shell or the Azure CLI. Using the Azure cloud shell, you can run the following steps to create a Virtual Machine. (Please note that this is also part of the subscription based plans on Azure, as you may be charged for creating Virtual )

*az vm create* \
   *--resource-group myResourceGroup1* \
   *--name myVM* \
   *--image UbuntuLTS* \
   *--admin-username azureuser* \
   *--generate-ssh-keys*

   above, i have specified the name of the vm, the resourcegroup which i want to store it, the image (we will talk more about images in the next lab), adminusername that allows the root user to sign into the vm, and an option to generate ssh keys for authentication which will also be spoken about in the next labs.

   ## 4. Open port 80 for web traffic 
   The virtual box(machine) comes with various ports which allow different kinds of connections.

Port 80 is used for inbound traffic. This means that users on the internet can communicate with your compute instance via that port.

Port 22 is used for ssh connections. This is to give remote access to your virtual box.

 Usually by default, the network protocol for each of this port is TCP.
 To open port 80 for web traffic, all i  need to do was run the command 

 *az vm open-port --port 80 --resource-group MyResourceGroup1 --name myVM* 

 Note(replace the name of the resource group and the name of the vm with the name you gave to them so that the code can run)

 ## 5. Connect to virtual machine
 The next thing to do is to connect to the VM or SSh into the VM as an administrator. recall that while we were creating the VM in step 3, we added a command (--generate-ssh-keys) this generates an authentication key that grants us secure connection into our VM (more about ssh will be discussed in upcoming labs). To ssh into the VM, all I need do is to run the ssh command like this,

 
 *ssh (adminusername)@public_ip_address*
 
 note that the public ip address was generated at the creation of the VM so all i need to do is to copy the ip and paste here and connect to the VM

 ## 6. Install web server 
 The virtual machine does not automatically come with a server installed. To install a web server on the platform, i ran the command 
 
  *sudo apt-get -y install apacehe2*

This installs the latest version of apache server on your VM since the VM is to be used as a web server.

## 7. View Web Server In Action 
To do this, I just need to go my VM  and click the external IP address. It would redirect me to a URL which I would use to view my installed apache2 web page.


# Below are some screenshots 
![create a resource group](https://i.imgur.com/EOhV6A4.jpg)

![create a Virtual machine](https://i.imgur.com/v9gSJXw.jpg)

![Open port 80 for web traffic](https://i.imgur.com/u7ID7H7.jpg)

![Connect to the vm](https://i.imgur.com/tyHd5Nr.jpg)

![Install Web server](https://i.imgur.com/ks0Z6Mv.jpg)

![Install web server 2](https://i.imgur.com/2i3uE9b.jpg)

![View Web server in action](https://i.imgur.com/VR4d1Sf.jpg)

