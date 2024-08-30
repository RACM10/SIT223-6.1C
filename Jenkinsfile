pipeline {
    agent any

    tools {
        // Ensure Maven and Git are installed and configured in Jenkins
        pipeline maven API // Replace with the configured Maven name
        git plugin 
    }

    stages {
        stage('Checkout') {
            steps {
                // Ensure the correct Git installation is used
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                // Use Maven for build
                bat 'mvn clean package'  // Use 'bat' for Windows
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Use JUnit or any other testing framework
                bat 'mvn test'  // Use 'bat' for Windows
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                // Use a tool like SonarQube
                bat 'mvn sonar:sonar'  // Use 'bat' for Windows
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                // Use a tool like OWASP Dependency Check
                bat 'mvn dependency-check:check'  // Use 'bat' for Windows
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                withCredentials([sshUserPrivateKey(credentialsId: 'staging-ssh-key', keyFileVariable: 'SSH_KEY')]) {
                    bat 'scp -i %SSH_KEY% target/*.jar user@staging-server:/path/to/deploy'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                bat 'curl -X POST http://staging-server/run-tests'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                withCredentials([sshUserPrivateKey(credentialsId: 'production-ssh-key', keyFileVariable: 'SSH_KEY')]) {
                    bat 'scp -i %SSH_KEY% target/*.jar user@production-server:/path/to/deploy'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }

        success {
            emailext to: 's223353507@deakin.edu.au',
                     subject: "Pipeline succeeded",
                     body: "Pipeline finished successfully",
                     attachLog: true
        }

        failure {
            emailext to: 's223353507@deakin.edu.au',
                     subject: "Pipeline failed",
                     body: "Pipeline failed. Please check the logs.",
                     attachLog: true
        }
    }
}
