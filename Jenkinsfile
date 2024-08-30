pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                bat 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                bat 'mvn test'
            }
            post {
                always {
                    emailext (
                        to: "wangzhi1757@gmail.com",
                        subject: "Test Phase - Build #${env.BUILD_NUMBER} - ${currentBuild.result}",
                        body: '''<html>
                                    <body>
                                        <p>Build Status: ${currentBuild.result}</p>
                                        <p>Build Number: ${env.BUILD_NUMBER}</p>
                                        <p>Check the <a href="${env.BUILD_URL}">console output</a>.</p>
                                     </body>
                                 </html>''',
                        attachLog: true,
                        mimeType: 'text/html'
                    )
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code...'
                bat 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                bat 'mvn org.owasp:dependency-check-maven:check'
            }
            post {
                always {
                    emailext (
                        to: "wangzhi1757@gmail.com",
                        subject: "Security Scan - Build #${env.BUILD_NUMBER} - ${currentBuild.result}",
                        body: '''<html>
                                    <body>
                                        <p>Build Status: ${currentBuild.result}</p>
                                        <p>Build Number: ${env.BUILD_NUMBER}</p>
                                        <p>Check the <a href="${env.BUILD_URL}">console output</a>.</p>
                                     </body>
                                 </html>''',
                        attachLog: true,
                        mimeType: 'text/html'
                    )
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                echo 'Simulating deployment to AWS EC2 instance...'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                echo 'Simulating integration testing...'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                echo 'Simulating deployment to AWS EC2 instance...'
            }
        }
    }

    post {
        success {
            emailext (
                to: 'wangzhi1757@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' Success",
                body: """<p>Build was successful!</p>
                         <p>Job Name: ${env.JOB_NAME}</p>
                         <p>Build Number: ${env.BUILD_NUMBER}</p>
                         <p>Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                         <p>Please check the Jenkins console output for more details.</p>""",
                mimeType: 'text/html'
            )
        }
        failure {
            emailext (
                to: 'wangzhi1757@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' Failure",
                body: """<p>Build failed.</p>
                         <p>Job Name: ${env.JOB_NAME}</p>
                         <p>Build Number: ${env.BUILD_NUMBER}</p>
                         <p>Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                         <p>Please check the Jenkins console output for more details.</p>""",
                mimeType: 'text/html'
            )
        }
    }
}
