# Docker image jfrog artifactory intigration using jenkins declarative pipeline

### Pipeline stages 




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
        DOCKER_IMAGE = '$BUILD_NUMBER'
        ARTIFACTORY_SERVER = 'https://ajtestjfrog.jfrog.io'
        ARTIFACTORY_REPO = 'docker-jfrog'
        JFROG_TOKEN = credentials('admin1-token')
    }
    tools{
        maven 'M2'
    }
    stages{
        stage ('Code Checkout'){
            steps{
                git 'https://github.com/anand40090/springboot-maven-course-micro-svc.git'
            }
        }
        stage ('Code build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage ('Package'){
            steps {
                sh 'mvn package'
             }
        }
        stage ('Docker Build'){
            steps{
                script{
                    sh "docker build -t $DOCKER_IMAGE ."
                }
            }
        }
        stage ('Push docker image to Jfrog') {
            steps{
                script{
                withCredentials([string(credentialsId: 'admin1-token', variable: 'JFROG_TOKEN')])
                {
                    sh "docker login https://ajtestjfrog.jfrog.io -u admin1 -p $JFROG_TOKEN"
                }
            }
            script{
                sh "docker tag $DOCKER_IMAGE ajtestjfrog.jfrog.io/$ARTIFACTORY_REPO/$DOCKER_IMAGE:$DOCKER_IMAGE"
                sh "docker push ajtestjfrog.jfrog.io/$ARTIFACTORY_REPO/$DOCKER_IMAGE:$DOCKER_IMAGE"
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
