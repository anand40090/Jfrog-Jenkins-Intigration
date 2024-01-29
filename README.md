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
2. Install the required softwares - 1] Docker engine 2] Apache Maven 3] Java 4] AWS Cli 5] Jfrog Cli 6] Jenkins 7] Docker compose
3. Configure the Jenkins with the requires plugins - 1] Apache Maven 2] Articatory plugins
4. Configure Jfrog for integration - 1] Create user with admin rights 2] Create access token for admin user 3] Create artifacts repository 
