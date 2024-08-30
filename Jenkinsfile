pipeline {
    agent any
    stages {
        stage('Send Email') {
            steps {
                script {
                    emailext(
                        subject: "Test Email",
                        body: "This is a test email.",
                        to: "kalanafathima3969@gmail.com"
                    )
                }
            }
        }
    }
}
