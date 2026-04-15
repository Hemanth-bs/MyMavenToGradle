pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {

        stage('Checkout SCM') {
            steps {
                git 'https://github.com/Hemanth-bs/MyMavenToGradle.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Using Java:"'
                sh 'java -version'
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
