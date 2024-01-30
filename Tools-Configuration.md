# Configure Apache Maven and JfrogArtifcatory in Jenkins

## 1. Install Maven and Artifactory plugins in Jenkins

 - Navigate to Dashboard >> Manage Jenkins >> Plugins

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/4d6f7aa7-28e6-446e-a906-e4c5b0f83e7f)


## 2. Configure Maven tool in Jenkins 

- Navigate to Dashboard >> Manage Jenkins >> Tools >> Find out the Maven installations
   - Specify the name for your Maven tool, define the Maven home folder path from the system where you have installed the maven
   - Make a note of the Maven installation name, it will be used in declarative pipeline. In this case the name is "M2"

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/dac9b049-fa98-4324-898c-9066617d46b4)

## 3. Configure Jfrog tool in Jenkins 

- Navigate to Dashboard >> Manage Jenkins >> System >> Find out for Jfrog
  - Specify the Instance id and make a note of it, it will be used in declarative pipeline.
  - User Jfrog Username and Password to authenticate with Jfrog server
  - Use youe Jfrog UI URL for connection 

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/9661d6a5-28b8-487f-befc-338452b06d16)

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/2790e961-30af-47b5-9bba-d6edc033fe55)

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/7ead7944-787f-434d-a415-89fc137a255e)




