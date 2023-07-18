pipeline {
    agent {
        label 'docker && linux && maven'
    }
    environment {
        webServerIP = "10.128.0.33"
    }

    stages {
        stage('CheckoutSCM') {
            steps {
                checkout scmGit(branches: [[name: '*/CI-CD-docker-java-deploy-dockerhub']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Admiralissimus/git-actions-jenkins-yandex-cloud-learning']])
            }
        }
        stage('MavenBuild') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('DockerBuild') {
            steps {
                sh 'docker build -t "admiralissimus/docker-web-java:v$BUILD_NUMBER" -t "admiralissimus/docker-web-java:latest" .'
            }
        }
        stage('DockerPush') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DockerHubToken', passwordVariable: 'DockerHubPwd', usernameVariable: 'DockerHubUser')]) {
                    sh 'docker login -u "$DockerHubUser" -p "$DockerHubPwd" '
                }
                sh 'docker push "admiralissimus/docker-web-java:v$BUILD_NUMBER"'
                sh 'docker push "admiralissimus/docker-web-java:latest"'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['test_2']) {
                    sh '''
                        [ -d ~/.ssh ] || mkdir ~/.ssh && chmod 0700 ~/.ssh
                        ssh-keyscan -t rsa,dsa ${webServerIP} >> ~/.ssh/known_hosts
                        ssh ubuntu@${webServerIP} docker rm -f java-web || true
                        ssh ubuntu@${webServerIP} docker pull admiralissimus/docker-web-java:latest
                        ssh ubuntu@${webServerIP} docker run --name java-web -p 8888:8080 -d admiralissimus/docker-web-java:latest
                    '''
                }
            }
        }
    }
}
