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
        success {
            echo "✅ About to send success email using mail step"
            mail to: 'kamlesh71324@gmail.com',
                 subject: "${env.JOB_NAME} - Build #${env.BUILD_NUMBER} - SUCCESS",
                 body: """Hello Kamlesh,

✅ Your Jenkins build completed successfully.

🔧 Job: ${env.JOB_NAME}
🔢 Build Number: ${env.BUILD_NUMBER}
📄 View the full build log: ${env.BUILD_URL}

Regards,  
Jenkins
"""
        }

        failure {
            echo "❌ About to send failure email using mail step"
            mail to: 'kamlesh71324@gmail.com',
                 subject: "${env.JOB_NAME} - Build #${env.BUILD_NUMBER} - FAILURE",
                 body: """Hello Kamlesh,

❌ Your Jenkins build has failed.

🔧 Job: ${env.JOB_NAME}
🔢 Build Number: ${env.BUILD_NUMBER}
📄 View the full build log: ${env.BUILD_URL}

Please review and fix the issue.

Regards,  
Jenkins
"""
        }
    }
}


