pipeline {
    agent any

    environment {
        RECIPIENTS = 'kalanafathima3969@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application with Maven...'
                // Example:mvn clean package
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests with JUnit and TestNG...'
                // Example:mvn test
            }
            post {
                success {
                    emailext(
                        to: "${env.RECIPIENTS}",
                        subject: "Unit and Integration Tests - Success",
                        body: """The Unit and Integration Tests stage completed successfully.
                                See attached log for details.""",
                        attachLog: true,
                        compressLog: true
                    )
                }
                failure {
                    emailext(
                        to: "${env.RECIPIENTS}",
                        subject: "Unit and Integration Tests - Failure",
                        body: """The Unit and Integration Tests stage failed.
                                 See attached log for details.""",
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code with SonarQube...'
                // Example:sonar-scanner
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan with OWASP Dependency-Check...'
                // Example:dependency-check --project your-project
            }
            post {
                success {
                    emailext(
                        to: "${env.RECIPIENTS}",
                        subject: "Security Scan - Success",
                        body: """The Security Scan stage completed successfully.
                                See attached log for details.""",
                        attachLog: true,
                        compressLog: true
                    )
                }
                failure {
                    emailext(
                        to: "${env.RECIPIENTS}",
                        subject: "Security Scan - Failure",
                        body: """The Security Scan stage failed.
                                 See attached log for details.""",
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment on AWS EC2...'
                // Example:AWS EC2
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging with Selenium/TestNG...'
                // Example:mvn verify -Pstaging
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment on AWS EC2...'
            }
        }
    }

    post {
        always {
            echo 'Sending final notification email...'
            emailext(
                to: "${env.RECIPIENTS}",
                subject: "Pipeline ${env.JOB_NAME} - Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                body: """Pipeline ${env.JOB_NAME} - Build #${env.BUILD_NUMBER} completed with status: ${currentBuild.currentResult}
                        See attached log for details.""",
                attachLog: true,
                compressLog: true
            )
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
