# Jfrog-Jenkins-Intigration

> In this repo, Jfrog has been integrated with Jenkins CI-CD pipeline

> we will be talking about How to Integrate JFrog Artifactory using Declarative Pipeline in Jenkins. 
> We will be having a pipeline created from scratch using a Jenkinsfile, and we will explain the whole syntax in each and every stage in this pipeline. 
> Also, in this pipeline we will create a .war file (web archive) and push that file to the JFrog artifactory.

### What is Jfrog artifactory
> JFrog Artifactory is a universal DevOps solution that manages and automates artifacts and binaries from start to finish during the application delivery process. 
> It gives you the option to choose from 25+ software build packages, all major CI/CD systems, and other existing DevOps tools.

_____________________________________________________________________________________________________________________________________________________________________________________________

# High level steps 

1. Create EC2 instance, in this case I am using Ubuntu 22.04
2. Install the required softwares in the system - 1] Docker engine 2] Apache Maven 3] Java 4] AWS Cli 5] Jfrog Cli 6] Jenkins 7] Docker compose
3. Configure the Jenkins with the requires plugins for this integration - 1] Apache Maven 2] Articatory plugins
4. Configure Jfrog for integration - 1] Create user with admin rights 2] Create access token for admin user 3] Create artifacts repository 

___________________________________________________________________________________________________________________________________________________________________________________________

# 1. Create EC2 instance

Step 1: Sign in to the AWS Management Console

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/2e8be038-b80f-4b6a-a74c-0669ffa9f1cf)


To create an EC2 instance, you first need to sign in to the AWS Management Console. 
If you don't already have an AWS account, you'll need to create one. Once you're signed in, navigate to the EC2 dashboard and Launch an instance.

Step 2: Choose a name of your instance

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/70841fbf-a5e8-482b-b050-2133f4a9edf4)

Select a name of your instance as per your likability

Step 3: Choose an Amazon Machine Image (AMI)

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/dc08dd8a-41f4-4f25-9f5c-26d6810b976e)

An Amazon Machine Image (AMI) is a pre-configured virtual machine that serves as a template for your EC2 instance. 
You'll be prompted to choose an AMI from a list of available options. You can choose from Amazon Linux, Ubuntu, Windows, and many other options.

Step 4: Choose an Instance Type

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/185baee5-307b-4a3b-a989-d26f2d58907f)

An instance type determines the computing resources (CPU, RAM, storage, etc.) available to your EC2 instance. 
There are a variety of instance types to choose from, ranging from small and low-cost to large and high-performance. 
Select the instance type that best fits your needs and budget.

Step 5: Create a key pair

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/64e819ab-7b82-46ba-9569-6b9f1d491986)

Create a key pair if you have never created one and store it in a safe place because it will act as a key to log in to your instance.

Step 6: Configure Security Group

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/5f03ea75-3fc6-40fc-a1cf-011334d4a95d)

Security groups act as virtual firewalls for your EC2 instance, controlling inbound and outbound traffic. 
You can configure security groups to allow or deny traffic from specific IP addresses, protocols, and ports. 
In this step, you'll need to create a new security group or select an existing one.

Step 7: Add Storage

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/5bbf6bca-6bbc-4443-a6e6-45937dc38f26)

EC2 instances require storage for the operating system, applications, and data. 
In this step, you can add and configure storage volumes for your instance. 
You can choose from different types of storage, including Amazon Elastic Block Store (EBS) volumes and instance store volumes.

Step 8: Review and Launch

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/940531d8-8dd5-4b77-b6c5-2301f48e8cfb)

Before launching your instance, review all the details to make sure everything is correct. 
You can also modify any settings that need to be changed. Once you're ready, click the "Launch" button to start your EC2 instance.

Step 9: Connect to Your Instance

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/9ea55df4-f66a-4478-837e-033632a3c4f4)

After launching your instance, you can connect to it using various methods, such as SSH or Remote Desktop Protocol (RDP). 
You can also use the AWS Systems Manager Session Manager to connect to your instance securely without the need for a public IP address.

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/8866e733-fe83-4850-a3d6-9e624ead0016)

__________________________________________________________________________________________________________________________________________________________________________________________

# 2. Install the required softwares in the system

Now run below codes to setup prerqusites softwares for the jfrog intgration 
Install the required softwares in the system - 1] Docker engine 2] Apache Maven 3] Java 4] AWS Cli 5] Jfrog Cli 6] Jenkins 7] Docker compose
Install Docker engine and Openjdk-11
```
sudo apt install docker.io openjdk-11-jdk -y
//This will install docker engine and openjdk-11

```

### Install Apache Maven to build the project (jar file), 
go to the apache maven website https://maven.apache.org/download.cgi for the required version of the software
```
sudo wget https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.zip
// to download the maven-3.9.6 version zip file

sudo apt install unzip
// to install the unzip tool

sudo unzip apache-maven-3.9.6-bin.zip
// to unzip the dowanloaded zip file

sudo mv apache-maven-3.9.6 /opt/
// to move the apache maven folder to OPT directory

M2_HOME=/opt/apache-maven-3.9.6
//Setting M2_HOME and Path Variables

export PATH="$M2_HOME/bin:$PATH"
// Exporting the maven path in user profile

mvn -version
//  To check the maven version 
```

### Let us get the installation done for AWS CLI 2.
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
// To download the AWS Cli -v2 zip file

unzip awscliv2.zip
// To unzip the downloaded AWSCLI file

sudo ./aws/install
// To install the AWS CLI file

aws --version
// To check the AWS CLI version
```

### Let us install Jenkins
```
// First, add the repository key to your system:
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key |sudo gpg --dearmor -o /usr/share/keyrings/jenkins.gpg

//Next, let’s append the Debian package repository address to the server’s sources.list:
sudo sh -c 'echo deb [signed-by=/usr/share/keyrings/jenkins.gpg] http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

//After both commands have been entered, run apt update so that apt will use the new repository.
sudo apt update
sudo apt install jenkins

//now that Jenkins is installed, start it by using systemctl:
sudo systemctl start jenkins.service

//Since systemctl doesn’t display status output, we’ll use the status command to verify that Jenkins started successfully:
sudo systemctl status jenkins

//To set up a UFW firewall, visit Initial Server Setup with Ubuntu 22.04, Step 4- Setting up a Basic Firewall.
By default, Jenkins runs on port 8080. Open that port using ufw:
sudo ufw allow 8080

//Open a web browser, and navigate to your server' IP address. Use the following syntax:
http://ip_address_or_domain:8080

```
![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/bd4d3fe5-6805-41d5-8de4-8ca4029f5951)

A page opens prompting you to Unlock Jenkins. Obtain the required administrator password in the next step.

2. Obtain the default Jenkins unlock password by opening the terminal and running the following command:

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/5d4def90-a67c-4003-a11f-ac484bf9dac0)

3. The system returns an alphanumeric code. Enter that code in the Administrator password field and click Continue.

4. The setup prompts to either Install suggested plugins or Select plugins to install. It’s fine to simply install the suggested plugins.

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/28542b80-9274-4c64-9792-40731ff7f03e)


