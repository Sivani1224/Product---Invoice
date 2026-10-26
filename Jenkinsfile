
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code is available in the workspace'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }
    }

    post {
        always {
            junit testResults: '**/target/surefire-reports/TEST-*.xml',
                  allowEmptyResults: true
        }

        success {
            echo 'CI Pipeline completed successfully!'
            archiveArtifacts artifacts: '**/target/*.jar',
                             allowEmptyArchive: true
        }

        failure {
            echo 'CI Pipeline failed. Check the console output.'
        }
    }
}
