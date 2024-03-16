pipeline {
    agent any
    
    stages {
        stage('Clone repository') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/CIVILIFIER/PES2UG22CS824_jenkins']]])
            }
        }
        
        stage('Build') {
            steps {
                build 'PES2UG22CS824-1'
                sh 'g++ main.cpp -o output'
            }
        }
        
        stage('Test') {
            steps {
                sh './output'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'deploy'
                // Add deployment steps here
            }
        }
    }
    
    post {
        failure {
            echo 'Pipeline failed'
        }
    }
}
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
                url: 'https://github.com/CIVILIFIER/PES2UG22CS824_jenkins'
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
                sh 'docker build -t CIVILIFIER/PES2UG22CS824:$BUILD_NUMBER .'
                sh 'docker push CIVILIFIER/PES2UG22CS824:$BUILD_NUMBER'
            }
        }
    }
}
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
                echo 'Build stage Successful'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                echo 'Test Stage Successful'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'mvn deploy'
                echo 'Deployment Successful'
            }
        }
    }
    post {
        failure {
            echo 'Pipeline failed'
        }
    }
}
