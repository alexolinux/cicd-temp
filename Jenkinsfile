pipeline {
    agent any

    stages {
        stage("Docker Build Image") {
            steps {
                sh 'echo "Build Docker Image..."'
                //sh 'docker build -t "alexmbarbosa/node-dockgen:latest" .'
            }
        }

        stage('Docker Push Image') {
            steps {
                script {
                    sh 'echo "Pushing Docker Image..."'
                    //sh 'docker push "alexmbarbosa/node-dockgen:latest"'                    
                }
            }
        }

        stage('Kube Deploy') {
            steps {
                sh 'echo "Kubernetes Deployment..."'
                //script {
                    //withKubeConfig([credentialsId: 'kubeconfig-credentials-id', serverUrl: 'kube-api-server-url']) {
                    //    sh 'kubectl apply -f kubernetes/deployment.yaml'
                    //}
                //}
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded.'
        }
    }
}
