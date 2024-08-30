pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Add your build steps here, e.g., compiling code
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Add your test steps here, e.g., running unit tests
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add your deployment steps here, e.g., deploying code to a server
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
                mimeType: 'text/html'
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
                mimeType: 'text/html'
            )
        }
    }
}

