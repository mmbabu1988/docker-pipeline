pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('mmbabu88-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/mmbabu1988/docker-pipeline.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t mmbabu88/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push mmbabu88/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

