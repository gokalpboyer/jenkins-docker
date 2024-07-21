pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('ayoub-dockerhub')
    }
    stages { 
        stage('Build docker image') {
            steps {  
                sh 'docker build -t aerradi/flask:$BUILD_NUMBER .'
            }
        }
        stage('Login to DockerHub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push image') {
            steps {
                sh 'docker push aerradi/flask:$BUILD_NUMBER'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
