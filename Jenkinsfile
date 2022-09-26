pipeline {
    agent any
    tools{
        maven 'maven-3.8.6'
        
    }
    environment {
        registry = "651308448971.dkr.ecr.ap-south-1.amazonaws.com/javaapp"
        registryCredential = 'AKIAZPJICHTF7A7QUDAM'
        dockerImage = ""
    }
    stages{
        stage('Build The Package'){
            steps{
                sh 'mvn clean package'
            }
        }
         
        stage('Building Image'){
            steps{
                script{
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Pushing Image in ECR'){
            steps{
                script{
                    docker.withRegistry('https://651308448971.dkr.ecr.ap-south-1.amazonaws.com', 'ecr:ap-south-1:AKIAZPJICHTF7A7QUDAM'){
                    dockerImage.push()
                    }
                }

            }
        }
    }
    post {
     
         success {  
             mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: 'amierkkhan@gmail.com', mimeType: 'text/html', replyTo: '', subject: "success CI: Project name -> ${env.JOB_NAME}", to: "amierkkhan@gmail.com";  
         }  
         failure {  
             mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: 'amierkkhan@gmail.com', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "amierkkha@gmail.com";  
         } 
    }
}
