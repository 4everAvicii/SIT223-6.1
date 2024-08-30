pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'mvn clean package'  // 使用Maven进行构建
            }
        }
        
        stage('Test') {
            steps {
                echo 'Running Unit and Integration Tests...'
                sh 'mvn test'  // 运行单元测试
                // 你可以在这里添加更多的集成测试步骤
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing Code...'
                sh 'mvn sonar:sonar'  // 使用SonarQube进行代码分析
                // 可以根据需求更改为你使用的其他代码分析工具
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                sh 'mvn dependency-check:check'  // 使用OWASP Dependency-Check进行安全扫描
                // 你也可以选择其他安全扫描工具，如 Snyk
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                sh 'scp target/*.jar user@staging-server:/path/to/staging/'  // 部署到预生产服务器
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                sh 'mvn verify -Dtest=StagingTestSuite'  // 在预生产环境中运行集成测试
                // 替换为实际的集成测试命令
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                sh 'scp target/*.jar user@production-server:/path/to/production/'  // 部署到生产服务器
            }
        }
    }

    post {
        // Send an email when the build is successful
        success {
            emailext (
                to: 'wangzhi1757@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' Success",
                body: """<p>Build was successful!</p>
                         <p>Job Name: ${env.JOB_NAME}</p>
                         <p>Build Number: ${env.BUILD_NUMBER}</p>
                         <p>Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                         <p>Please check the Jenkins console output for more details.</p>""",
                mimeType: 'text/html',
            )
        }
        // Send an email when the build fails
        failure {
            emailext (
                to: 'wangzhi1757@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' Failure",
                body: """<p>Build failed.</p>
                         <p>Job Name: ${env.JOB_NAME}</p>
                         <p>Build Number: ${env.BUILD_NUMBER}</p>
                         <p>Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                         <p>Please check the Jenkins console output for more details.</p>""",
                mimeType: 'text/html',
            )
        }
    }
}