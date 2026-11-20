pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out GitHub repository...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Starting build...'
                sh 'python3 --version'
            }
        }

        stage('Execute Script') {
            steps {
                sh 'python3 hello.py'
            }
        }
    }

    
post {
    always {
        emailext(
            to: 'nilavarasanswathi@gmail.com',
            subject: "Jenkins Build: ${currentBuild.currentResult} - ${env.JOB_NAME}",
            body: """
Hello,

Your GitHub commit triggered an automatic Jenkins build.

Project: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build Status: ${currentBuild.currentResult}

Build URL: ${env.BUILD_URL}

Please find the complete console output attached.

Regards,
Jenkins CI/CD Automation
""",
            attachLog: true
        )
    }
}
}


