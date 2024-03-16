pipeline {
    agent {
        docker {
            image 'node:14'
        }
    }
    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main', url: 'https://github.com/CIVILIFIER/PES2UG22CS824_jenkins.git'
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
                script {
                    def dockerImage = docker.build("CIVILIFIER/PES2UG22CS824:${env.BUILD_NUMBER}")
                    dockerImage.push()
                }
            }
        }
    }
}

