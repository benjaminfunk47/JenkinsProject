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
                    withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                        bat "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    }                
                }
            }
        }
        stage('Benjamin Gambill - Push image to Dockerhub'){
            steps{
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                        bat 'docker push bengambill/jenkinsproject:latest'
                    }
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
