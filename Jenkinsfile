pipeline {
    
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build'
                echo 'Task: Build the code using a build automation tool'
                echo 'Tools: Maven, Gradle, Ant'
                // Add your actual build commands here, e.g., sh 'mvn clean install'
            }
            post {
                failure {
                    emailext (
                        to: 'omarseyam1729@gmail.com',
                        subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Build Stage",
                        body: "Build failed. Please check the logs for details.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests'
                echo 'Task: Run unit tests and integration tests'
                echo 'Tools: JUnit, TestNG, Selenium, Mockito'
                sh 'echo "Running unit tests..." > unit-tests.log'
                // Add actual test commands here, e.g., sh 'mvn test'
                sh 'echo "Tests completed successfully." >> unit-tests.log'
            }
            post {
                always {
                    def buildStatus = currentBuild.result ?: 'SUCCESS'
                    def subject = "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} - Unit and Integration Tests ${buildStatus}"
                    def body = """
                    Unit and Integration Tests Status: ${buildStatus}
                    Job: ${env.JOB_NAME}
                    Build Number: ${env.BUILD_NUMBER}
                    """

                    emailext (
                        to: 'omarseyam1729@gmail.com',
                        subject: subject,
                        body: body,
                        attachmentsPattern: 'unit-tests.log'
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis'
                echo 'Task: Analyze code quality and adherence to industry standards'
                echo 'Tools: SonarQube, Checkstyle, PMD, SpotBugs'
                // Add actual code analysis commands here, e.g., sh 'sonar-scanner'
            }
            post {
                failure {
                    emailext (
                        to: 'omarseyam1729@gmail.com',
                        subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Code Analysis Stage",
                        body: "Code analysis failed. Please check the logs for details.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan'
                echo 'Task: Scan the code for security vulnerabilities'
                echo 'Tools: Snyk, OWASP Dependency-Check, Veracode'
                sh 'echo "Running security scan..." > security-scan.log'
                // Add actual security scan commands here, e.g., sh 'snyk test'
                sh 'echo "Security scan completed successfully." >> security-scan.log'
            }
            post {
                always {
                    def buildStatus = currentBuild.result ?: 'SUCCESS'
                    def subject = "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} - Security Scan ${buildStatus}"
                    def body = """
                    Security Scan Status: ${buildStatus}
                    Job: ${env.JOB_NAME}
                    Build Number: ${env.BUILD_NUMBER}
                    """

                    emailext (
                        to: 'omarseyam1729@gmail.com',
                        subject: subject,
                        body: body,
                        attachmentsPattern: 'security-scan.log'
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging'
                echo 'Task: Deploy the application to a staging environment'
                echo 'Tools: AWS EC2, Docker, Kubernetes'
                // Add your actual deployment commands here
            }
            post {
                failure {
                    emailext (
                        to: 'omarseyam1729@gmail.com',
                        subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Deploy to Staging Stage",
                        body: "Deployment to staging failed. Please check the logs for details.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging'
                echo 'Task: Run integration tests in the staging environment'
                echo 'Tools: Selenium, Cypress, Postman, Cucumber'
                // Add your actual test commands here
            }
            post {
                failure {
                    emailext (
                        to: 'omarseyam1729@gmail.com',
                        subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Integration Tests Stage",
                        body: "Integration tests on staging failed. Please check the logs for details.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production'
                echo 'Task: Deploy the application to the production server'
                echo 'Tools: AWS EC2, Docker, Kubernetes, Ansible'
                // Add your actual deployment commands here
            }
            post {
                failure {
                    emailext (
                        to: 'omarseyam1729@gmail.com',
                        subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} Failed at Deploy to Production Stage",
                        body: "Deployment to production failed. Please check the logs for details.",
                        attachLog: true
                    )
                }
            }
        }
    }
    post {
        always {
            def buildStatus = currentBuild.result ?: 'SUCCESS'
            def subject = "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} - ${buildStatus}"
            def body = """
            Build Status: ${buildStatus}
            Job: ${env.JOB_NAME}
            Build Number: ${env.BUILD_NUMBER}
            """

            emailext (
                to: 'omarseyam1729@gmail.com',
                subject: subject,
                body: body,
                attachLog: true
            )
        }
    }
}
