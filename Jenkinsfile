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
                echo 'Running Unit and Integration Tests...'
                bat 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis...'

                bat 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'

                bat 'dependency-check.bat --project "MyProject" --scan .'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'

                bat 'scp target/myapp.jar user@staging-server:/path/to/deploy/'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                bat 'ssh user@staging-server "cd /path/to/deploy && java -jar myapp.jar && run-tests.sh"'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                bat 'scp target/myapp.jar user@production-server:/path/to/deploy/'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished. Sending notifications...'

            mail to: '1305975121@qq.com',
                 subject: "Pipeline ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                 body: "The pipeline has completed with status: ${currentBuild.currentResult}."
        }
    }
}
