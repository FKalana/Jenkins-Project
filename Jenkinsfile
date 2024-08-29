pipeline {
    agent any
    environment {
        DIRECTORY_PATH = '/Users/fathimakalana/.jenkins/workspace/Jenkins Project'
        TESTING_ENVIRONMENT = 'TestEnv'
        PRODUCTION_ENVIRONMENT = 'KProduction'
    }
 
    stages {
        stage('Build') {
            steps {
                echo "Building the code using Maven..."
                echo "Fetching source code from ${DIRECTORY_PATH}"
                echo "Compiling the code and generating artifacts..."
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Unit tests"
                echo "Integration tests"
            }
        }
        stage('Code Analysis') {
            steps {
                echo "Check the quality of the code"
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploy the application to a testing environment specified by the environment variable: ${env.TESTING_ENVIRONMENT}"
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests in Staging environment..."
            }
        }
        stage('Approval') {
            steps {
                script {
                    input message: 'Approve deployment to production?'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploy the code to the production environment: ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
    }
    post {
        success {
            mail to: 'kalanafathima3969@gmail.com',
                 subject: "Build Successful: ${currentBuild.fullDisplayName}",
                 body: "The pipeline completed successfully. View details at ${env.BUILD_URL}"
        }
        failure {
            mail to: 'kalanafathima3969@gmail.com',
                 subject: "Build Failed: ${currentBuild.fullDisplayName}",
                 body: "The pipeline failed. View details at ${env.BUILD_URL}"
        }
    }
}
