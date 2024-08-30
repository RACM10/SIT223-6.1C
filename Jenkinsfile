pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Use Maven for build
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Use JUnit or any other testing framework
                sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                // Use a tool like SonarQube
                sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                // Use a tool like OWASP Dependency Check
                sh 'mvn dependency-check:check'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Example of deployment command to an EC2 instance
                sh 'scp target/*.jar user@staging-server:/path/to/deploy'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Example of running integration tests on staging
                sh 'curl -X POST http://staging-server/run-tests'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Example of deployment command to an EC2 instance
                sh 'scp target/*.jar user@production-server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }

        success {
            mail to: 'youremail@example.com',
                 subject: "Pipeline succeeded",
                 body: "Pipeline finished successfully",
                 attachLog: true
        }

        failure {
            mail to: 's223353507@deakin.edu.au',
                 subject: "Pipeline failed",
                 body: "Pipeline failed. Please check the logs.",
                 attachLog: true
        }
    }
}
