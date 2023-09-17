pipeline {
    agent any

    environment {
        DOCKERHUB_CREDS = creadentials('dockerhub')
    }

    stages {
        stage('Clone repo'){
            steps {
                checkout scm
                sh 'ls *'
            }
        }

        stage('Build image'){
            steps {
                sh 'docker build -t ayushkavad/express-app:$BUILD_NUMBER ./'
            }
        }

        stage('Docker login'){
            steps {
                sh 'echo $DOCKERHUB_CREDS_PSW | docker login -u $DOCKERHUB_CREDS_USR --password-stdin' 
            }
        }


        stage('Push image'){
            steps {
                sh 'docker push ayushkavad/express-app:$BUILD_NUMBER' 
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}