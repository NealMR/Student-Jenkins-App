pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building web application...'
                bat 'dir'
                echo 'Build completed!'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing web application...'
                bat 'if exist index.html (echo index.html found) else (exit /b 1)'
                bat 'if exist style.css (echo style.css found) else (exit /b 1)'
                bat 'if exist script.js (echo script.js found) else (exit /b 1)'
                echo 'All required files are present.'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying web application...'

                bat '''
                if not exist C:\\JenkinsDeploy mkdir C:\\JenkinsDeploy
                xcopy /Y /I index.html C:\\JenkinsDeploy
                xcopy /Y /I style.css C:\\JenkinsDeploy
                xcopy /Y /I script.js C:\\JenkinsDeploy
                '''

                echo 'Deployment completed!'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check console output.'
        }
    }
}
