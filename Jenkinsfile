
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
                subject: "Jenkins Build: ${currentBuild.currentResult}",
                body: """
Hello,

A new GitHub commit triggered the Jenkins pipeline.

Project: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build Status: ${currentBuild.currentResult}
Build URL: ${env.BUILD_URL}

Console Output:
${currentBuild.rawBuild.getLog(100).join('\n')}

Regards,
Jenkins CI/CD
""",
                to: 'nilavarasan914@gmail.com'
            )
        }
    }
}

