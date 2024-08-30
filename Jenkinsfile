pipeline {
    agent any
 
    environment {
        RECIPIENTS = 'kalanafathima3969@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application with Maven...'
                // Example: sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests with JUnit and TestNG...'
                // Example: sh 'mvn test'
            }
            post {
                success {
                    emailext(
                        to: "${env.RECIPIENTS}",
                        subject: "Unit and Integration Tests - Success",
                        body: """<p>The Unit and Integration Tests stage completed successfully.</p>
                                <p>See attached log for details.</p>""",
                        attachLog: true,
                        compressLog: true
                    )
                }
                failure {
                    emailext(
                        to: "${env.RECIPIENTS}",
                        subject: "Unit and Integration Tests - Failure",
                        body: """<p>The Unit and Integration Tests stage failed.</p>
                                <p>See attached log for details.</p>""",
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code with SonarQube...'
                // Example: sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan with OWASP Dependency-Check...'
                // Example: sh 'dependency-check --project your-project'
            }
            post {
                success {
                    emailext(
                        to: "${env.RECIPIENTS}",
                        subject: "Security Scan - Success",
                        body: """<p>The Security Scan stage completed successfully.</p>
                                <p>See attached log for details.</p>""",
                        attachLog: true,
                        compressLog: true
                    )
                }
                failure {
                    emailext(
                        to: "${env.RECIPIENTS}",
                        subject: "Security Scan - Failure",
                        body: """<p>The Security Scan stage failed.</p>
                                <p>See attached log for details.</p>""",
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment on AWS EC2...'
                // Example: sh 'scp target/app.war user@staging-server:/path/to/deploy'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging with Selenium/TestNG...'
                // Example: sh 'mvn verify -Pstaging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment on AWS EC2...'
                // Example: sh 'scp target/app.war user@production-server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            echo 'Sending final notification email...'
            emailext(
                to: "${env.RECIPIENTS}",
                subject: "Pipeline ${env.JOB_NAME} - Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                body: """<p>Pipeline ${env.JOB_NAME} - Build #${env.BUILD_NUMBER} completed with status: ${currentBuild.currentResult}</p>
                        <p>See attached log for details.</p>""",
                attachLog: true,
                compressLog: true
            )
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
