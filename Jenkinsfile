pipeline{
    agent any
     
    }
    stages{
        stage('build'){
            steps{
            sh "docker build -t galalshalaby/e-commerce:${env.BUILD_NUMBER} ."
            withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'pass', usernameVariable: 'user')]) {
             sh "docker login -u $user  -p $pass"
             sh "docker push  galalshalaby/e-commerce:${env.BUILD_NUMBER}"
                //dasdasdsads
}
            }
       
           
        }

        stage('deploy'){
            steps{
                sh "docker run -d -p 500${env.BUILD_NUMBER}:8080 galalshalaby/e-commerce:${env.BUILD_NUMBER}"
            }
        }
    }
}
