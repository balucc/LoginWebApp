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
    }    
}
