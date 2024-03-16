pipeline {
    agent any
    
    stages {
        stage('Clone repository') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '**/main']], 
                          userRemoteConfigs: [[url: 'https://github.com/CIVILIFIER/PES2UG22CS824_jenkins']]])
            }
        }
        
        stage('Build') {
            steps {
                // Assuming hello.cpp is in the root of your repository
                build 'PES2UG22CS824-1'
                sh 'g++ main/hello.cpp -o output'
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
            }
        }
    }
    
    post {
        failure {
            echo 'Pipeline failed'
        }
    }
}
