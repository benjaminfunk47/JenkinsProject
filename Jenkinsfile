pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker_hub_login')
    }
    stages{
        stage('Benjamin Gambill - Build Docker Image'){
            steps{
                sh 'docker build -t bengambill/jenkinsproject:latest .'
            }
        }
        stage('Benjamin Gambill - Login to Dockerhub'){
          steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --pasword-stdin'
            }
        }
        stage('Benjamin Gambill - Push image to Dockerhub'){
            steps{
                sh 'docker push bengambill/jenkinsproject:latest'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
