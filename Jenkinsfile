pipeline {
    agent any

    stages {

        stage('Checkout SCM') {
            steps {
                git 'https://github.com/Hemanth-bs/GradleSeleniumApp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'chmod +x gradlew'
                sh './gradlew clean build'
            }
        }

        stage('Test (Selenium)') {
            steps {
                sh './gradlew test'
            }
        }

        stage('Report') {
            steps {
                junit '**/build/test-results/test/*.xml'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed'
        }
        failure {
            echo 'Build or tests failed!'
        }
        success {
            echo 'Build successful!'
        }
    }
}
