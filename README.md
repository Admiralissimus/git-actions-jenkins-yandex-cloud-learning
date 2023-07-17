# git-actions-jenkins-yandex-cloud-learning
In this project I am going to improve my skills in 
- CI/CD
- jenkins
- docker
- yandex.cloud
- dockerhub
- webhook
- build java

This is CI/CD project (without testing part).
This pipeline (deploy-java.job) downlads from github source code.
Builds docker image and pushes it in DockerHub.
Image from docker hub is deployed to the server with docker engine.
Uses webhook for automatic deploy.
