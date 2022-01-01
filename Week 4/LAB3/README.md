# Lab 3: Deploy a containerized application with AWS Copilot

1. Install the AWS Copilot CLI.
2. Install and configure the AWS CLI.
3. Run aws configure to set up a default profile that the AWS Copilot CLI will use to manage your application and services.
4. Install and run Docker. 

### Notes:

Deploy a containerized application with AWS Copilot
* https://docs.aws.amazon.com/AmazonECS/latest/developerguide/getting-started-aws-copilot-cli.html


# NOTES FROM MY EXPERIENCE WITH LAB 3
## First lets do some Basic Definition

1. The AWS-Copilot CLI is a tool for developers to build, release, and operate production-ready containerized applications on AWS App Runner, Amazon ECS, and AWS Fargate.
From getting started, pushing to staging, and releasing to production, Copilot can help manage the entire lifecycle of your application development.

2. Docker is a technology that provides the tools for you to build, run, test, and deploy distributed applications that are based on Linux containers. Amazon ECS uses Docker images in task definitions to launch containers as part of tasks in your clusters.

3. A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. 

4. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings. Amazon ECS task definitions use Docker images to launch containers on the container instances in your clusters

 ## Then we move on to pactically installing aws copilot and install/run a docker on an instance created.

### 1. Create a new instance.
Create a new instance using the AWS CLI(cloudshell) by using the AWS ec2 run-instances command, include the image id, the instance type and the key pair which will be used to ssh into the Instance. For example i created this instance
    
    aws ec2 run-instances \
    --image-id ami-0abcdef1234567890 \
    --instance-type t2.micro \
    --key-name MyKey1

### 2. Open Port 22 and port 80 for traffic
Port 22 is used to connect into the instance created and is only accesible to the host IP address ONLY. Port 80 on the other hand allows for web traffic. i.e it allows other users on the internet to have access and view the content of our server.
    
    To do this, i went to the ec2 portal and clicked on the instance, then scrolled down to "security" and clicked on edit inbound rules and from there I opened port 22 and port 80 for web traffic.

### 3. Connect to the instance
i was able to ssh into my vm through the key pair i had created for the purpos of this new instance. i ran this code to connect to my instance 

    ssh -i "Mykey1.pem" ec2-user@ec2-54-68-7-232.us-west-2.compute.amazonaws.com

### 4. Update the installed packages and package cache on your instance.
To do this i ran this code 

    sudo yum update -y

### 5. Install the AWS Copilot CLI 
Next thing i did was to install the aws copilot into the linux machine just created and updated. to this this i ran th ecode;
    
    sudo curl -Lo /usr/local/bin/copilot https://github.com/aws/copilot-cli/releases/latest/download/copilot-linux \
    && sudo chmod +x /usr/local/bin/copilot \
    && copilot --help

### 6. Install and configure the AWS CLI.
Installing and configuring the AWS CLI involves the following steps 
    
    I. Download the installation file using this curl command 
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

    II. Unzip the installer using this unzip command 
    unzip awscliv2.zip

    III. Run the installed program using this command 
    sudo ./aws/install

    IV. Verify that the AWS CLI has been installed by running this command 
    aws --version

    V. Next is to set up the AWS CLI that has just been installed and to do that run the code 

    aws configure

    Then I was prompted to submit four important credentials 

    - Access key ID
    - Secret access key
    - AWS Region
    - Output format

    Afrter doing this succesfully, I moved next to installing and running docker and docker images 

### 7. Install and run Docker 
i followed the below steps to install docker on my Amazon Linux 2 Machine

    I. Install the most recent Docker Engine package by running the code;
    sudo amazon-linux-extras install docker

    II. Start and enable the Docker service by running the codes;
    sudo systemctl start docker
    sudo systemctl enable docker

    (The second line of code is necesaary for docker to survive a rebbot of the instance if there is a cause for it)

    III. next is to add the ec2 user to the docker group so that i can execute Docker commands without using sudo and that was done by running the code;
    sudo usermod -a -G docker ec2-user

    after doing this at first it didnt work but when i logged out and logged back in, it worked perfectly fine and i could run codes on this machine without using sudo

### 8. Create a Docker Image
i followed the below steps to create a docker image 

    I. I Created a file called Dockerfile.
    (A Dockerfile is a manifest that describes the base image to use for my Docker image and what I want installed and running on it). I was able to do this by running the code;
    touch Dockerfile

    II. i Edited the Dockerfile ijust created and added the following content.

    FROM ubuntu:18.04

    # Install dependencies
    RUN apt-get update && \
    apt-get -y install apache2

    #  Install apache and write hello world message
    RUN echo 'Hello World MY Name is Mr Right and I am here to take over the world!' > /var/www/html/index.html

    # Configure apache
    RUN echo '. /etc/apache2/envvars' > /root/run_apache.sh && \
    echo 'mkdir -p /var/run/apache2' >> /root/run_apache.sh && \
    echo 'mkdir -p /var/lock/apache2' >> /root/run_apache.sh && \ 
    echo '/usr/sbin/apache2 -D FOREGROUND' >> /root/run_apache.sh && \ 
    chmod 755 /root/run_apache.sh

    EXPOSE 80
    CMD /root/run_apache.sh

    [This Dockerfile uses the Ubuntu 18.04 image. The RUN instructions update the package caches, install some software packages for the web server, and then write the "Hello World MY Name is Mr Right and I am here to take over the world!" content to the web server's document root. The EXPOSE instruction exposes port 80 on the container, and the CMD instruction starts the web server.]

    III. I Built the Docker image from my Dockerfile using the code;
    docker build -t hello-world .

    IV. Next thing i did was to verify that the image was created succesfully and to do that i simply rAN THIS CODE;
    docker images --filter reference=hello-world
    I got the expected output and i moved on to run the newly built image using the command;
    docker run -t -i -p 80:80 hello-world
    [ The -p 80:80 option maps the exposed port 80 on the container to port 80 on the host system.]

    Next thing i did was to paste my public ip adress on my browser and a web page came up with the "Hello World MY Name is Mr Right and I am here to take over the world!" statement
## Below is a screenshot of the above output
![](https://i.imgur.com/zekSPIV.jpg)