pipeline {
    agent any

    stages {
        stage("Docker Build Image") {
            steps {
                script {
                    dockerapp = sh(script: '/usr/bin/docker build -t alexmbarbosa/node-dockgen:latest --file ./Dockerfile .', returnStatus: true)
                    //dockerapp = docker.build("alexmbarbosa/node-dockgen:latest", "--file ./Dockerfile .")
                }
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
