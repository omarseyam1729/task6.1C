pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven'
                // For example: sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests using JUnit and integration tests using TestNG'
                // For example: sh 'mvn test'
                // For integration tests: sh 'mvn verify'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code using SonarQube'
                // For example: sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP Dependency-Check'
                // For example: sh 'dependency-check.sh'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying application to staging server (AWS EC2 instance)'
                // Example deployment command, such as using AWS CLI
                // sh 'aws deploy create-deployment --application-name MyApp --deployment-group-name Staging --s3-location bucket=my-bucket,key=my-app.zip'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment'
                // Example integration test commands
                // sh 'run-integration-tests.sh'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying application to production server (AWS EC2 instance)'
                // Example deployment command
                // sh 'aws deploy create-deployment --application-name MyApp --deployment-group-name Production --s3-location bucket=my-bucket,key=my-app.zip'
            }
        }
    }

    post {
        always {
            emailext(
                subject: "Pipeline ${currentBuild.currentResult}: ${currentBuild.fullDisplayName}",
                body: "Build result: ${currentBuild.currentResult}\n\nSee logs at ${env.BUILD_URL}",
                recipientProviders: [[$class: 'Developers']],
                attachmentsPattern: '**/test-*.log'
            )
        }
    }
}