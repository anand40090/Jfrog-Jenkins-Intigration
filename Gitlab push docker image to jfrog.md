# Gitlab push docker image to jfrog
> In this example we will build the project and push the docker image to Jfrog from Gitlab

### Prerequisites
1. Docker engine
2. Latest Gitlab Docker image


# Run the gitlab Using Docker Compose

[Follow to install and configure gitlab using docker & Docker Compose](https://docs.gitlab.com/ee/install/docker.html)

In this lab I have used docker compose to create the docker container 
```
docker-compose.yml

version: '3.6'
services:
  gitlab:
    image: gitlab/gitlab-ce:latest
    container_name: gitlab
    restart: always
    hostname: 'gitlab.example.com'
    ports:
      - '80:80'
      - '443:443'
      - '22:22'
    volumes:
      - '$GITLAB_HOME/config:/etc/gitlab'
      - '$GITLAB_HOME/logs:/var/log/gitlab'
      - '$GITLAB_HOME/data:/var/opt/gitlab'
    shm_size: '256m'

```

Once docker container is up, run the below mentioned command to get the default root password 

Default user is root and I have reset password "Hp@123!@#"
```
sudo docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password

```

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/f7e0a5b8-5e8b-43fe-9fae-4708b8a38091)

![image](https://github.com/anand40090/Jfrog-Jenkins-Intigration/assets/32446706/738c2b4d-49a7-4ba4-9572-a20cdb4a1a13)




