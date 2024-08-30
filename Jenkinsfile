pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // 使用Maven进行构建
                sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // 使用JUnit运行测试
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'
                // 使用SonarQube进行代码分析
                // 在此步骤中，可以添加对SonarQube扫描的调用
                sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // 使用OWASP Dependency-Check进行安全扫描
                // 可以在此步骤中调用相关的安全扫描工具
                sh 'dependency-check.sh --project "MyProject" --scan .'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // 部署到预备环境（例如AWS EC2实例）
                // 这里可以调用部署脚本或使用工具进行部署
                sh 'scp target/myapp.jar user@staging-server:/path/to/deploy/'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // 在预备环境中运行集成测试
                sh 'ssh user@staging-server "cd /path/to/deploy && java -jar myapp.jar && run-tests.sh"'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // 部署到生产环境
                sh 'scp target/myapp.jar user@production-server:/path/to/deploy/'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished. Sending notifications...'
            mail to: 'your-email@example.com',
                 subject: "Pipeline ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                 body: "The pipeline has completed with status: ${currentBuild.currentResult}.",
                 attachLog: true
        }
    }
}
