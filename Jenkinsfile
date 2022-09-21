pipeline {
    agent any

    stages {
        stage(maven){
            steps{
                sh 'mvn clean install -DskipTests'
            }
        }
        stage('Docker') {
            steps{
                sh 'docker build -t realtime .'
            }
        }
        stage('Docker login') {
            steps{
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 976842334971.dkr.ecr.us-east-1.amazonaws.com'
            }
        }         
        
        stage('Docker tag') {
            steps{
                sh 'docker tag realtime:latest 976842334971.dkr.ecr.us-east-1.amazonaws.com/docker:latest'
            }
        }
        stage('Docker push') {
            steps{
                sh 'docker push 976842334971.dkr.ecr.us-east-1.amazonaws.com/docker:latest'
            }
        } 
        
     }
 }
