pipeline {
    agent any
    
    environment {
        COMMIT_MESSAGE = ''
        BUILD_LOG = 'build_log.txt'
    }
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                    sh "echo 'Checkout completed at $(date)' >> ${BUILD_LOG}"
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    sh "echo 'Building the code...' >> ${BUILD_LOG}"
                    COMMIT_MESSAGE = sh(returnStdout: true, script: 'git log -1 --pretty=%B').trim()
                    sh "echo 'Commit message: ${COMMIT_MESSAGE}' >> ${BUILD_LOG}"
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                sh "echo 'Running Unit and Integration Tests...' >> ${BUILD_LOG}"
            }
        }
        stage('Code Analysis') {
            steps {
                sh "echo 'Running Code Analysis...' >> ${BUILD_LOG}"
            }
        }
        stage('Security Scan') {
            steps {
                sh "echo 'Running Security Scan...' >> ${BUILD_LOG}"
            }
        }
        stage('Deploy to Staging') {
            steps {
                sh "echo 'Deploying to Staging...' >> ${BUILD_LOG}"
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                sh "echo 'Running Integration Tests on Staging...' >> ${BUILD_LOG}"
            }
        }
        stage('Deploy to Production') {
            steps {
                sh "echo 'Deploying to Production...' >> ${BUILD_LOG}"
            }
        }
    }
    
    post {
        always {
            script {
                sh "echo 'Pipeline finished at $(date)' >> ${BUILD_LOG}"
            }
            archiveArtifacts artifacts: "${BUILD_LOG}", allowEmptyArchive: true
        }
        failure {
            script {
                emailext (
                    to: 'omarseyam1729@gmail.com',
                    subject: "Jenkins Build Failed: ${env.BUILD_ID}",
                    body: """Build ${env.BUILD_ID} failed.
                    Commit message: ${COMMIT_MESSAGE}
                    Check Jenkins for details.""",
                    attachmentsPattern: "${BUILD_LOG}"
                )
            }
        }
        success {
            script {
                emailext (
                    to: 'omarseyam1729@gmail.com',
                    subject: "Jenkins Build Success: ${env.BUILD_ID}",
                    body: """Build ${env.BUILD_ID} completed successfully.
                    Commit message: ${COMMIT_MESSAGE}""",
                    attachmentsPattern: "${BUILD_LOG}"
                )
            }
        }
    }
}
