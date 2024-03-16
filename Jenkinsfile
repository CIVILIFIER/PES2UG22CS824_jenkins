pipeline {
    agent {
        docker {
            image 'node:14'
        }
    }
    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main',
                url: 'https://github.com/CIVILIFIER/PES2UG22CS824_jenkins.git'
            }
        }
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build application') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Test application') {
            steps {
                sh 'npm test'
            }
        }
        stage('Push Docker image') {
            steps {
                sh "docker build -t CIVILIFIER/PES2UG22CS824-1:$BUILD_NUMBER ."
                sh "docker push CIVILIFIER/PES2UG22CS824-1:$BUILD_NUMBER"
            }
        }
    }
}
