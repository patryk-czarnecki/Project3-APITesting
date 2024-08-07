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
        
        stage('Archive Results and Documentation') {
            steps {
                archiveArtifacts artifacts: 'reports/*.html'                
            }
        }
    }

    post {
        always {
            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'reports',
                reportFiles: 'postman_test_report.html',
                reportName: 'Postman Test Report'
            ])            
        }
    }
}
