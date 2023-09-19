pipeline {
    agent any
    environment {
        DOCKERHUB_CREDS = credentials('dockerhub')
    }
    stages {
        stage('Clone Repo') {
            steps {
                checkout scm
                sh 'ls *'
            }
        }
        stage('Build Image') {
            steps {
                script {
                    sh "docker build -t ayushkavad/jenkinstest:$BUILD_NUMBER ./"
                }
            }
        }
        stage('Docker Login') {
            steps {
                script {
                    def DOCKERHUB_CREDS_USR = credentials('dockerhub').username
                    def DOCKERHUB_CREDS_PSW = credentials('dockerhub').password
                    sh "echo $DOCKERHUB_CREDS_PSW | docker login -u $DOCKERHUB_CREDS_USR --password-stdin"
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    sh "docker push ayushkavad/jenkinstest:$BUILD_NUMBER"
                }
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
