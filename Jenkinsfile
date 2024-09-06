pipeline {
    agent any
    
    environment {
        COMMIT_MESSAGE = ''
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the code...'
                script {
                    COMMIT_MESSAGE = sh(returnStdout: true, script: 'git log -1 --pretty=%B').trim()
                    echo "Commit message: ${COMMIT_MESSAGE}"
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline finished!'
            // Archive the console log
            script {
                writeFile file: 'build.log', text: currentBuild.rawBuild.log
                archiveArtifacts artifacts: 'build.log', allowEmptyArchive: true
            }
        }
        failure {
            emailext (
                to: 'omarseyam1729@gmail.com',
                subject: "Jenkins Build Failed: ${env.BUILD_ID}",
                body: """Build ${env.BUILD_ID} failed.
                Commit message: ${COMMIT_MESSAGE}
                Check Jenkins for details.""",
                attachLog: true
            )
        }
        success {
            emailext (
                to: 'omarseyam1729@gmail.com',
                subject: "Jenkins Build Success: ${env.BUILD_ID}",
                body: """Build ${env.BUILD_ID} completed successfully.
                Commit message: ${COMMIT_MESSAGE}""",
                attachLog: true
            )
        }
    }
}