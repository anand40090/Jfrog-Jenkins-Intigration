# 2. Install the required softwares in the system

Now run below codes to setup prerqusites softwares for the jfrog intgration 

### Install Docker engine and Openjdk-11
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
### Let us install Jfrog CLI
```
wget -qO - https://releases.jfrog.io/artifactory/jfrog-gpg-public/jfrog_public_gpg.key | sudo apt-key add -
// To add the Jfrog reposiroty key in user profile

echo "deb https://releases.jfrog.io/artifactory/jfrog-debs xenial contrib" | sudo tee -a /etc/apt/sources.list &&    sudo apt update &&
// Download the Jfrog reposiroty and install it

sudo apt install -y jfrog-cli-v2-jf &&
// To install the jfrog cli

jf intro
jf --version
// To check the jfrog version
```

### Let us install Jenkins

```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key |sudo gpg --dearmor -o /usr/share/keyrings/jenkins.gpg
// First, add the repository key to your system:

sudo sh -c 'echo deb [signed-by=/usr/share/keyrings/jenkins.gpg] http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
//Next, let’s append the Debian package repository address to the server’s sources.list:

sudo apt update
sudo apt install jenkins
//After both commands have been entered, run apt update so that apt will use the new repository.

sudo systemctl start jenkins.service
//now that Jenkins is installed, start it by using systemctl:

sudo systemctl status jenkins
//Since systemctl doesn’t display status output, we’ll use the status command to verify that Jenkins started successfully:

sudo ufw allow 8080
//To set up a UFW firewall, visit Initial Server Setup with Ubuntu 22.04, Step 4- Setting up a Basic Firewall.
By default, Jenkins runs on port 8080. Open that port using ufw:

http://ip_address_or_domain:8080
//Open a web browser, and navigate to your server' IP address. Use the following syntax:


```
![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/bd4d3fe5-6805-41d5-8de4-8ca4029f5951)

A page opens prompting you to Unlock Jenkins. Obtain the required administrator password in the next step.

2. Obtain the default Jenkins unlock password by opening the terminal and running the following command:

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/5d4def90-a67c-4003-a11f-ac484bf9dac0)

3. The system returns an alphanumeric code. Enter that code in the Administrator password field and click Continue.

4. The setup prompts to either Install suggested plugins or Select plugins to install. It’s fine to simply install the suggested plugins.

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/28542b80-9274-4c64-9792-40731ff7f03e)
