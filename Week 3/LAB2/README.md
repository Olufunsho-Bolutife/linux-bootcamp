# Lab 2: Install a LAMP stack on an Azure Linux VM

1. Prepare the LAMP server
2. Test your Lamp server
3. Secure the database server
4. (Optional) Install phpMyAdmin

### Notes:

Tutorial: Install a LAMP web server on the Amazon Linux AMI
* https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-LAMP.html

Tutorial: Host a WordPress blog on Amazon Linux 2
* https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/hosting-wordpress.html

Sample Gist
* https://gist.github.com/mikepfeiffer/c079608703e604224e58a3d40d0fa043#file-lamp-linux-aws-sh

# NOTES  From my LAB 2 Experience 

## 1. Prepare the LAMP server
Just like installing a LAMP stack (Linux, Apache, Mysql, PHP) on Azure, I was also able to do the same thing on Aws. You can either do it throught the GUI or through the CLI which in this case is the aws cloud shell

NOTE; I was able to install the LAMP stack using the following code on Amazon Linux Ami. To install the LAMP stack we must have a running instance and port 80 must have been opened because we are working to build a web server on the instance

I created my VM using an Amazon Linux Ami. I configured my security group to open port 80 for the web sever and port 22 for ssh authentication.

I was able to run this following command to install Apache, Mysql and PHP

*sudo yum install -y httpd24 php72 mysql57-server php72-mysqlnd*

This command installed the various extentions simultaneously.

*sudo service httpd start* 

 ( This is to start Apache web server after installation)

*sudo chkconfig httpd on* 

( This is to enable Apache web server to survive a reboot).
## 2. Test your Lamp server
I was able to test my various installed apps by using my public Ip.

For my PHP, to create a PHP file i ran this command as directed


*sudo sh -c 'echo "" > /var/www/html/info.php'*

After this i was able to view my PHP page online, while Apache was the Index html file, Php was the other page. I was able to put in *(my Ip address/info.php).*

## 3. Secure the database server
To secure my database which is MySql i ran the following command to start and secure Mysql

*sudo service mysqld start*-  (This is to start Mysql database)

*sudo mysql_secure_installation* - (This is to secure Mysql)

 I was able to set my password, disable the remote root login and i was able to remove the test database).