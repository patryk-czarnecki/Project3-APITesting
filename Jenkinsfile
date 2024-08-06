pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/patryk-czarnecki/Project3-APITesting.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install --legacy-peer-deps'
            }
        }

        stage('Run Postman Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Archive Results') {
            steps {
                archiveArtifacts artifacts: 'reports/*.html'
            }
        }
    }
}
