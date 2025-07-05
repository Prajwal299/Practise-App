pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "my-flask-app:${env.BUILD_NUMBER}"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'Prajwal299', url: 'https://github.com/Prajwal299/Practise-App.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build(DOCKER_IMAGE)
                }
            }
        }
        stage('Stop Previous Containers') {
            steps {
                sh '''
                docker ps -q -f name=my-flask-app | xargs --no-run-if-empty docker stop
                docker ps -a -q -f name=my-flask-app | xargs --no-run-if-empty docker rm
                '''
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    dockerImage.run('-p 5000:5000 --name my-flask-app -d')
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed.'
        }
        success {
            echo 'Flask app deployed successfully on port 5000.'
        }
        failure {
            echo 'Pipeline failed. Check the logs for details.'
        }
    }
}