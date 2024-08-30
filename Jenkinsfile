pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // 在这里添加你的构建步骤，例如编译代码
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // 在这里添加你的测试步骤，例如运行单元测试
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // 在这里添加你的部署步骤，例如将代码发布到服务器
            }
        }
    }

    post {
        // 构建成功时发送邮件
        success {
            emailext (
                to: 'wangzhi1757@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' 成功",
                body: """<p>构建成功！</p>
                         <p>项目名称: ${env.JOB_NAME}</p>
                         <p>构建编号: ${env.BUILD_NUMBER}</p>
                         <p>构建地址: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                         <p>详情请查看 Jenkins 控制台输出。</p>""",
                mimeType: 'text/html'
            )
        }
        // 构建失败时发送邮件
        failure {
            emailext (
                to: 'wangzhi1757@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' 失败",
                body: """<p>构建失败。</p>
                         <p>项目名称: ${env.JOB_NAME}</p>
                         <p>构建编号: ${env.BUILD_NUMBER}</p>
                         <p>构建地址: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                         <p>详情请查看 Jenkins 控制台输出。</p>""",
                mimeType: 'text/html'
            )
        }
    }
}
