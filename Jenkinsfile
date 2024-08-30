pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker_cred', toolName: 'docker') {
                        sh "docker build -t chuckbass11/frontend:latest ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker_cred', toolName: 'docker') {
                        sh "docker push chuckbass11/frontend:latest"
                    }
                }
            }
        }
    }
}
