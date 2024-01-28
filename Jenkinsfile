pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    docker.build("nodejs-portfolio:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    docker.image("nodejs-portfolio:${env.BUILD_NUMBER}").inside {
                        sh 'npm install'
                        sh 'node test.js'
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // Your Kubernetes deployment steps here
                script {
                    def kubeconfig = readFile "${WORKSPACE}/path/to/your/kubeconfig"
                    withKubeConfig(credentialsId: 'your-kube-config-credentials-id', kubeconfigText: kubeconfig) {
                        sh 'kubectl apply -f kubernetes-deployment.yaml'
                    }
                }
            }
        }
    }
}
