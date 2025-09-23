pipeline {
    agent{
        label 'master'
    }
    stages {
        stage('pull src code') {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/AhmedElhagrasi/flask_app.git'
            }
        }
        
        stage('build docker image'){
            steps{
                sh "docker build -t ahmedelhagrasi/flask_app:$BUILD_NUMBER ."
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
    sh "docker login -u $USER -p $PASS"
    sh "docker push ahmedelhagrasi/flask_app:$BUILD_NUMBER"
}
            }
        }
        
        stage('test'){
            steps{
                echo "no test cases found"
            }
        }
        
        stage('deploy'){
            steps{
                sh "docker run -d -p 500$BUILD_NUMBER:8008 ahmedelhagrasi/flask_app:$BUILD_NUMBER"
            }
        }
    }
}
