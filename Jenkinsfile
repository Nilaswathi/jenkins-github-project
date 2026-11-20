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
        script {
            echo "Testing Jenkins email notifications..."

            // Test basic Jenkins email
            try {
                mail(
                    to: 'nilavarasanswathi@gmail.com',
                    subject: "Jenkins Basic Email - ${currentBuild.currentResult}",
                    body: """
                    Jenkins basic email test.

                    Project: ${env.JOB_NAME}
                    Build: ${env.BUILD_NUMBER}
                    Status: ${currentBuild.currentResult}
                    """
                )
                echo "Basic email step executed."
            } catch (err) {
                echo "Basic email failed: ${err}"
            }

            // Test Extended Email Plugin
            try {
                emailext(
                    to: 'nilavarasanswathi@gmail.com',
                    subject: "Jenkins Extended Email - ${currentBuild.currentResult}",
                    body: """
                    Jenkins extended email test.

                    Project: ${env.JOB_NAME}
                    Build: ${env.BUILD_NUMBER}
                    Status: ${currentBuild.currentResult}
                    Build URL: ${env.BUILD_URL}
                    """,
                    attachLog: true
                )
                echo "Extended email step executed."
            } catch (err) {
                echo "Extended email failed: ${err}"
            }
        }
    }
}

}


