# Docker image jfrog artifactory intigration using jenkins declarative pipeline

> In this Ci-CD jenkins pipeline, we are building Docker image and pushing it to Jfrog articatort as per the
> Jenkins build number.

### Pipeline stages 

1. Code Checkout
2. Code build
3. Code package
4. Docker image Build
5. Push docker image to Jfrog
6. post - Sucess or Failure notification


 ![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/88c2e5cc-7388-4d0e-80b6-db6e9bf59e75)

*********************************************************************************************

### Create docker repository on jfrog artifacts

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/a0caf5bc-89fa-46c0-b673-32b29de621bf)

###  Create Jfrog user token key for intgration with jenkins

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/3f0d07fd-ae40-42f8-a85b-22db294fc5e9)

### Configure Jfrog user token in Jenkins 

Jenkins Dashboard >> Manage Jenkins >>Credentials >>System >> Global credentials (unrestricted)

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/36df5d60-4967-4b6c-aba1-efb8f9dda1a4)

### Configure Jfrog system in Jenkins 

Jenkins Dashboard >> Manage Jenkins >> System

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/17599c20-0243-4f09-9fb8-2d9d9ce635cc)

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/1e251488-33c2-46e4-9da1-e4412e578b35)


### Working declarative code 
```
pipeline{
    agent any
    environment {
        DOCKER_IMAGE = '$BUILD_NUMBER \\ to capture the pipeline build number 
        ARTIFACTORY_SERVER = 'https://ajtestjfrog.jfrog.io' \\ Jfrog artifcatory URL
        ARTIFACTORY_REPO = 'docker-jfrog' \\ Repository name from Jfrog 
        JFROG_TOKEN = credentials('admin1-token') \\ User token for Jfrog authentication
    }
    tools{
        maven 'M2' \\ Maven tool configured on Ec2 instance to build the java code using Maven 
    }
    stages{
        stage ('Code Checkout'){
            steps{
                git 'https://github.com/anand40090/springboot-maven-course-micro-svc.git'
                \\ Git repository 
            }
        }
        stage ('Code build'){
            steps{
                sh 'mvn clean install'
                 \\ Shell command to run the Maven test for the Git reposirty Java code
            }
        }
        stage ('Package'){
            steps {
                sh 'mvn package'
                 \\ To build the Jar file from the Git code
             }
        }
        stage ('Docker Build'){
            steps{
                script{
                    sh "docker build -t $DOCKER_IMAGE ."
                     \\ To build the docker image as defined in the Dockerfile from the git reposiroty, docker image will be build
                        as per the jenkins $BUILD_NUMBER
                }
            }
        }
        stage ('Push docker image to Jfrog') {
            steps{
                script{
                withCredentials([string(credentialsId: 'admin1-token', variable: 'JFROG_TOKEN')])
                {
                    sh "docker login https://ajtestjfrog.jfrog.io -u admin1 -p $JFROG_TOKEN"
                    \\ Authenticate the Jfrog articatory using the User token veriable
                }
            }
            script{
                sh "docker tag $DOCKER_IMAGE ajtestjfrog.jfrog.io/$ARTIFACTORY_REPO/$DOCKER_IMAGE:$DOCKER_IMAGE"
                \\ Tag the docker image to be pushed on Jfrog 
                sh "docker push ajtestjfrog.jfrog.io/$ARTIFACTORY_REPO/$DOCKER_IMAGE:$DOCKER_IMAGE"
                 \\ Push the docker image on Jfrog
            }
            }
        }
    }
    post {
        success {
            echo 'Docker image successfully pushed to JFrog Artifactory!'
        }
        failure {
            echo 'Failed to push Docker image to JFrog Artifactory.'
        }
    }
}
```

### Output on jfrog 

In above pipeline it is configured to store the docker image as per the jenkins build number on jfrog artifact

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/43779421-4eda-40fc-add5-120995f7d8bc)
