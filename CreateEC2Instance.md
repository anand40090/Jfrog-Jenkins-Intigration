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

