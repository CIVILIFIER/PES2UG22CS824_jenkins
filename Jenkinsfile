
pipeline {
    agent {
        docker {
            image 'node:14'
        }
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/CIVILIFIER/PES2UG22CS824_jenkins.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build Application') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Test Application') {
            steps {
                sh 'npm test'
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    def buildNumber = env.BUILD_NUMBER
                    sh "docker build -t CIVILIFIER/<image>:$buildNumber ."
                    sh "docker push CIVILIFIER/<image>:$buildNumber"
                }
            }
        }
    }
    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
