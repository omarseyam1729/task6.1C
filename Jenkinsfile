pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Example: Save build logs to a file
                sh 'mvn clean package | tee build.log'
                archiveArtifacts artifacts: 'build.log', allowEmptyArchive: true
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Example: Save test logs to a file
                sh 'mvn test | tee test.log'
                archiveArtifacts artifacts: 'test.log', allowEmptyArchive: true
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                // Example: Save code analysis logs to a file
                sh 'sonar-scanner | tee code_analysis.log'
                archiveArtifacts artifacts: 'code_analysis.log', allowEmptyArchive: true
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                // Example: Save security scan logs to a file
                sh 'dependency-check --project JenkinsPipeline --scan ./ | tee security_scan.log'
                archiveArtifacts artifacts: 'security_scan.log', allowEmptyArchive: true
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Example: Save deployment logs to a file
                sh 'deploy_to_staging.sh | tee deploy_staging.log'
                archiveArtifacts artifacts: 'deploy_staging.log', allowEmptyArchive: true
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Example: Save integration test logs to a file
                sh 'run_integration_tests.sh | tee integration_tests_staging.log'
                archiveArtifacts artifacts: 'integration_tests_staging.log', allowEmptyArchive: true
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Example: Save deployment logs to a file
                sh 'deploy_to_production.sh | tee deploy_production.log'
                archiveArtifacts artifacts: 'deploy_production.log', allowEmptyArchive: true
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished!'
            archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
        }
        failure {
            emailext(
                to: 'omarseyam1729@gmail.com',
                subject: "Jenkins Build Failed: ${env.BUILD_ID}",
                body: "Build ${env.BUILD_ID} failed. Check Jenkins for details.",
                attachmentsPattern: '*.log'
            )
        }
        success {
            emailext(
                to: 'omarseyam1729@gmail.com',
                subject: "Jenkins Build Success: ${env.BUILD_ID}",
                body: "Build ${env.BUILD_ID} completed successfully.",
                attachmentsPattern: '*.log'
            )
        }
    }
}
