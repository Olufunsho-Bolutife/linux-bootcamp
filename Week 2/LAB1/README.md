# Lab 1: Create a Linux virtual machine with the AWS CLI

1. Launch AWS Cloud Shell
3. Create virtual machine
4. Open port 80 for web traffic
5. Connect to virtual machine
6. Install web server
7. View the web server in action

### Notes:

Quickstart: Create a Linux VM
* https://aws.amazon.com/getting-started/launch-a-virtual-machine-B-0/

Quickstart for AWS CloudShell
* https://docs.aws.amazon.com/cloudshell/latest/userguide/working-with-cloudshell.html

# Notes from My LAB 1 Experience 

## 1. Launch AWS Cloud Shell
Just like the Azure portal the Aws console also has the icon to click on to lunch the cloud shell basically a straight-forward procedure. I went ahead and lunched the Aws cloud shell on my console using bash. Although we can choose from any of the shell avaliable which are pre-installed on the Aws cloud shell by just using example;

pwsd-for powershell

bash- for bash.

## 2. Create virtual machine
The Aws virtual machine can be created basically using two procedures

The GUI 

The command line. I used both for the creation of my VMs. I used the Cli to create a VM by using various commands for example, I ran this code on the CLI to create my first VM

*aws ec2 run instance* \

*--image-id ami-0abcdef1234567890* \

*--instance-type t2.micro* \

*--key-name My-ssh-key*



## 3. Open port 80 for web traffic
Port 80 is default for web traffic. it is the port that allows the public have access to the web server to fetch information from the server. If the Vm is created to allows web server then port 80 needs to be opened for traffic. I opened port 80 on my already craeted using the interface. clicked on security group, then to the inbound rule, I opened a new inbound rule to allow HTTP and port 80 was opened.

## 4. Connect to virtual machine
I ssh into my Virtual machine using the ssh client(windows terminal). I copied the key on the interface and opened it on my local bash where the key is located and i was able to connect to my VM.

5. Install web server
I was able to install a web server (apache2) using the following command;

*yum update -y* \

*sudo yum install -y httpd (apache2)* \

*sudo systemctl start httpd* \

*sudo systemctl enable httpd*

(sudo systemctl enable httpd  was added To enable the server to survive a reboot).

## 6. View the web server in action
I copied my Ip address generated and pasted it on google and i was able to see my installed apache2.