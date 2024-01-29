pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out the source code from GitHub
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Set up Node.js environment
                    tool 'node-dockgen'
                    
                    // Build Docker image
                    sh 'docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .'
                }
            }
        }

        stage('Push Registry') {
            steps {
                script {
                    // Push Docker image to a container registry
                    sh 'docker push ${DOCKER_IMAGE}:${DOCKER_TAG}'
                }
            }
        }

        stage('Kube Deploy') {
            steps {
                script {
                    // Deploy to Kubernetes using kubectl
                    withKubeConfig([credentialsId: 'kubeconfig-credentials-id', serverUrl: 'kube-api-server-url']) {
                        sh 'kubectl apply -f kubernetes/deployment.yaml'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded.'
        }
    }
}
