pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven...'
                // Example tool: Maven
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit...'
                // Example tool: JUnit for unit tests, Selenium for integration tests
            }
            post {
                success {
                    emailext(
                        subject: "Unit and Integration Tests Successful - ${currentBuild.fullDisplayName}",
                        body: "The Unit and Integration Tests stage has completed successfully.",
                        to: "rabailaamir993@gmail.com",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        subject: "Unit and Integration Tests Failed - ${currentBuild.fullDisplayName}",
                        body: "The Unit and Integration Tests stage has failed. Please check the attached logs for details.",
                        to: "rabailaamir993@gmail.com",
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code quality using SonarQube...'
                // Example tool: SonarQube
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP...'
                // Example tool: OWASP ZAP
            }
            post {
                success {
                    emailext(
                        subject: "Security Scan Successful - ${currentBuild.fullDisplayName}",
                        body: "The Security Scan stage has completed successfully.",
                        to: "kalanafathima3969@gmail.com",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        subject: "Security Scan Failed - ${currentBuild.fullDisplayName}",
                        body: "The Security Scan stage has failed. Please check the attached logs for details.",
                        to: "kalanafathima3969@gmail.com",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to the staging environment...'
                // Example environment: AWS EC2
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment using Selenium...'
                // Example tool: Selenium
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to the production environment...'
                // Example environment: AWS EC2
            }
        }
    }

    post {
        always {
            echo 'Pipeline has completed.'
        }
    }
}
