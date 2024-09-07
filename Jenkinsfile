pipeline {
    agent any
    
    stages {
        stage('Send Email') {
            steps {
                emailext (
                    to: 'omarseyam1729@gmail.com',
                    subject: "Test Email from Jenkins",
                    body: "This is a test email from the Jenkins pipeline.",
                    mimeType: 'text/plain'
                )
            }
        }
    }
}
