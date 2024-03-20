# smile-jenkins

## Usage

1. Clone to local machine
2. Create a bridge network for docker: `docker network create jenkins`
3. Build with Dockerfile: `docker build -t myjenkins-blueocean:2.440.1-1 .`
4. Run your own image as a container:

```shell
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8081:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  --volume /Volumes/Data/smile-jenkins/jenkins_home:/var/jenkins_home
  myjenkins-blueocean:2.440.1-1
```

Get the Passowrd:

```shell
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
```

Connect to the jenkins:

```shell
https://localhost:8081/
```
