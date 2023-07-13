# git-actions-jenkins-yandex-cloud-learning
In this project I am going to improve my skills in 
- CI/CD
- jenkins
- docker
- yandex.cloud
- dockerhub
- webhook

This is CI/CD project (without testing part).

This pipeline (deploy-python.job) downlads from github a source code.

Builds a docker image and pushes it to the DockerHub.

The image from DockerHub is deployed to the server with a docker engine.

Uses webhook for automatic deploy.
