pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package'  // 实际构建命令
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'  // 运行单元测试和集成测试
            }
            post {
                always {
                    emailext (
                        to: "sandylilovehome@gmail.com",
                        subject: "Test Phase - Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                        body: '''<html>
                                    <body>
                                        <p>Build Status: ${currentBuild.currentResult}</p>
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
                sh 'mvn sonar:sonar'  // 运行代码分析命令
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh 'mvn org.owasp:dependency-check-maven:check'  // 运行安全扫描命令
            }
            post {
                always {
                    emailext (
                        to: "sandylilovehome@gmail.com",
                        subject: "Security Scan - Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                        body: '''<html>
                                    <body>
                                        <p>Build Status: ${currentBuild.currentResult}</p>
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
                echo 'Simulating deployment to AWS EC2 instance...'  // 模拟部署命令
                // 实际部署到预生产环境的命令
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                echo 'Simulating integration testing...'  // 模拟集成测试命令
                // 在预生产环境中运行集成测试的实际命令
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                echo 'Simulating deployment to AWS EC2 instance...'  // 模拟部署命令
                // 实际部署到生产环境的命令
            }
        }
    }

    post {
        success {
            emailext (
                to: 'sandylilovehome@gmail.com',
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
                to: 'sandylilovehome@gmail.com',
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
