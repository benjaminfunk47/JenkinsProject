pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker_hub_login')
    }
    stages{
        stage('Benjamin Gambill - Build Docker Image'){
            steps{
                script {
                    bat 'docker build -t bengambill/jenkinsproject:latest .'
                }
            }
        }
        stage('Benjamin Gambill - Login to Dockerhub'){
          steps{
                script {
                    bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }
        }
        stage('Benjamin Gambill - Push image to Dockerhub'){
            steps{
                script {
                    bat 'docker push bengambill/jenkinsproject:latest'
                }
            }
        }
    }
    post {
        always {
            script {
                bat 'docker logout'
            }
        }
    }
}
