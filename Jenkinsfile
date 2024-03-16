pipeline {
    agent any
    
    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main',
                url: 'https://github.com/CIVILIFIER/PES2UG22CS824_jenkins'
            }
        }
        
        stage('Build') {
            steps {
                // Assuming main.cpp is in the root of your repository
                sh 'g++ main.cpp -o output'
                echo 'Build stage Successful'
            }
        }
        
        stage('Test') {
            steps {
                sh './output'
                echo 'Test Stage Successful'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deployment'
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
