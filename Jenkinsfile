pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the source code from SCM...'
                // Simulating checkout (no actual code checkout)
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                echo 'mvn clean package'  // Simulate Maven build command
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                echo 'mvn test'  // Simulate Maven test command
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                echo 'mvn sonar:sonar'  // Simulate SonarQube analysis command
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                echo 'mvn dependency-check:check'  // Simulate OWASP Dependency Check command
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                echo 'scp -i %SSH_KEY% target/*.jar user@staging-server:/path/to/deploy'  // Simulate deployment to staging
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                echo 'curl -X POST http://staging-server/run-tests'  // Simulate integration tests on staging
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                echo 'scp -i %SSH_KEY% target/*.jar user@production-server:/path/to/deploy'  // Simulate deployment to production
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }

        success {
            echo 'Pipeline succeeded'
            emailext to: 'racm12.gaming@gmail.com',
                     subject: "Pipeline succeeded",
                     body: "Pipeline finished successfully",
                     attachLog: true
        }

        failure {
            echo 'Pipeline failed. Please check the logs.'
            emailext to: 'racm12.gaming@gmail.com',
                     subject: "Pipeline failed",
                     body: "Pipeline failed. Please check the logs.",
                     attachLog: true
        }
    }
}
