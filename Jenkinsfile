pipeline {
    agent any 
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dhanushkumar28-dockerhub')
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t dhanushkumar28/kaniyam:latest .' 
            }
        }
        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push dhanushkumar28/kaniyam:latest'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
