pipeline {
    agent any   
    stages {
        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                bat "docker build -t kubdemoapp:v1 ."
            }
        }
        stage('Docker Login') {
            steps {
                  bat 'docker login -u nayanika3664 -p Niharika@2010'
                }
            }
        stage('push Docker Image to Docker Hub') {
            steps {
                echo "push Docker Image to Docker Hub"
                bat "docker tag kubdemoapp:v1 nayanika3664/week8:kubeimage1"
                bat "docker push nayanika3664/week8:kubeimage1"
            }
        }
        stage('Deploy to Kubernetes') { 
            steps { 
                    // apply deployment & service 
                    bat 'kubectl apply -f deployment.yaml --validate=false' 
                    bat 'kubectl apply -f service.yaml' 
            } 
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}