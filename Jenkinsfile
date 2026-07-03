pipeline {
    agent none 
    
    stages {
        stage('Checkout SCM') {
            agent any 
            steps {
                checkout scm
            }
        }
        
        stage('Build & Test') {
            agent {
                docker { 
                    image 'node:7.8.0' 
                }
            }
            steps {
                echo 'Building NodeJS application...'
                sh 'npm install'
                echo 'Running tests...'
                sh 'npm test'
            }
        }
        
        stage('Docker build') {
            agent any 
            steps {
                script {
                    if (env.BRANCH_NAME == 'main') {
                        sh 'docker build -t nodemain:v1.0 .'
                    } else if (env.BRANCH_NAME == 'dev') {
                        sh 'docker build -t nodedev:v1.0 .'
                    }
                }
            }
        }
    }
}
