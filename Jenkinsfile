
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
            		subject: "Build ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            		body: """
    Build Status: ${currentBuild.currentResult}

    Project: ${env.JOB_NAME}
    Build Number: ${env.BUILD_NUMBER}
    Build URL: ${env.BUILD_URL}

    The complete Jenkins console output is attached.
            """,
            attachLog: true
        		)
    	       }
	}
}

