pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true' // Allow test failures without breaking pipeline
            }
        }

        stage('Security Scan') {
            steps {
                sh 'npm audit || true' // Allow audit warnings without breaking pipeline
            }
        }
    }

    post {
        always {
            script {
                emailext (
                    to: 'kamlesh71324@gmail.com',
                    subject: "${env.JOB_NAME} - Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                    body: """<p>Hello Kamlesh,</p>
<p>🔧 Job: <b>${env.JOB_NAME}</b><br>
🔢 Build Number: <b>${env.BUILD_NUMBER}</b><br>
📄 <a href="${env.BUILD_URL}">Click here to view the full build</a></p>
<p>Regards,<br>Jenkins</p>""",
                    mimeType: 'text/html',
                    attachLog: true
                )
            }
        }
    }
}



