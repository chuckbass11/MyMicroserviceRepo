pipeline {
    agent any

    stages {
        stage('Deploy to Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://BBFE71AC61BBE14EF9042ACA3FDAC6AF.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yml"
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://BBFE71AC61BBE14EF9042ACA3FDAC6AF.gr7.us-east-1.eks.amazonaws.com']]) {
                    script {
                        // Check the status of all resources in the namespace 'webapps'
                        sh "kubectl get all -n webapps"

                        // Optionally, you can add more checks to verify if the deployment rolled out successfully
                        // Example: Checking if deployment is available and ready
                        sh "kubectl rollout status deployment/<your-deployment-name> -n webapps"
                    }
                }
            }
        }
    }
}
