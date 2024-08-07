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

        stage('Run JMeter Tests') {
            steps {
                sh '/home/patryk-czarnecki/Pulpit/apache-jmeter-5.6.3/bin/jmeter -n -t jmeter/test_plan.jmx -l reports/jmeter_test_report.jtl'
            }
        }

        stage('Archive Results') {
            steps {
                archiveArtifacts artifacts: 'reports/*.html'
                archiveArtifacts artifacts: 'reports/jmeter_test_report.jtl'
            }
        }

        stage('Publish Performance Report') {
            steps {
                perfReport filterRegex: '', sourceDataFiles: 'reports/jmeter_test_report.jtl'
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
