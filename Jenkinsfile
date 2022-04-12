pipeline{
    agent any
    tools {
       maven 'maven3.8.5'
            }
    stages{
        stage('Git checkout'){
            steps{
              git 'https://github.com/balucc/LoginWebApp.git'
            }
        }
        stage('package application'){
            steps{
                sh 'mvn clean package'
            }
        stage('build docker image'){
            steps{
                sh 'docker build -t --name balucc/loginwebapp:${BUILD_ID} -f Dockerfile-tomcat .'
                sh 'docker build -t --name balucc/mysql:${BUILD_ID} -f Dockerfile-mysql .'
            } 
        }
        stage('Push Docker Image'){
            steps{
              withDockerRegistry(credentialsId: 'balu_dockerhub', url: 'https://hub.docker.com/repository/docker/balucc/loginwebapp') {
                sh 'docker push balucc/loginwebapp:${BUILD_ID}'
    }
}
            step{
               withDockerRegistry(credentialsId: 'balu_dockerhub', url: 'https://hub.docker.com/repository/docker/balucc/mysql') {
                   sh 'docker push balucc/mysql:${BUILD_ID}'

                }
            }
        }

        }
    }    
}
