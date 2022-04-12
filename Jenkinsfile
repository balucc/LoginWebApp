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
        }
        stage('build docker image'){
            steps{
                sh 'docker build -t balucc/loginwebapp:${BUILD_ID} -f Dockerfile-tomcat .'
                sh 'docker build -t balucc/mysql:${BUILD_ID} -f Dockerfile-mysql .'
            } 
        }
        stage('Push Docker Image'){
            steps{
              withDockerRegistry(credentialsId: 'balu_dockerhub', url: 'https://index.docker.io/v1/') {
                sh 'docker push balucc/loginwebapp:${BUILD_ID}'
                sh 'docker push balucc/mysql:${BUILD_ID}'  
    }
            }
        }
       
        }

        }
       

