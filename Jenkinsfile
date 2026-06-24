pipeline {
    agent any
    
    tools {
        maven 'Maven3'
        jdk 'Java21'
    }
    
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/aydindemir1/java-044-devops-hello']])
                bat 'mvn clean install'
            }
        }
        
        stage('Docker Image to DockerHub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
                        bat "docker login -u aydindemir -p ${dockerhub}"
                        bat 'docker build --build-arg JAR_FILE=target/devops-application.jar -t aydindemir/devops-application:latest .'
                        bat 'docker push aydindemir/devops-application:latest'
                    }
                }
            }
        }
    }
}