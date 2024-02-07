# Gitlab push docker image to jfrog
> In this example we will build the project and push the docker image to Jfrog from Gitlab

### Prerequisites
1. Docker engine
2. Latest Gitlab Docker image
3. 

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
