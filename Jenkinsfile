pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building the Docker image"
                sh "docker build -t galalshalaby/e-commerce:${env.BUILD_NUMBER} ."
                withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    echo "Logging in to Docker Hub"
                    sh "echo $pass | docker login -u $user --password-stdin"
                    echo "Pushing the Docker image to Docker Hub"
                    sh "docker push galalshalaby/e-commerce:${env.BUILD_NUMBER}"
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying the Docker container"
                sh "docker run -d -p 500${env.BUILD_NUMBER}:8080 galalshalaby/e-commerce:${env.BUILD_NUMBER}"
            }
        }
    }
}
