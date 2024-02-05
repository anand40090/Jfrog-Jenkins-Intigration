# Docker image jfrog artifactory intigration using jenkins declarative pipeline

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


### Working pipeline 
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
                 \\ Shell code to run the Maven test for the Git reposirty Java code
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
                     \\ To build the docker image as defined in the Dockerfile from the git reposiroty, docker file will be stored as 
                      per the jenkins $BUILD_NUMBER
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
