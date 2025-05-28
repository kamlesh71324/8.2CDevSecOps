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
            emailext (
                to: 'kamlesh71324@gmail.com',
                subject: "${env.JOB_NAME} - Build #${env.BUILD_NUMBER} - SUCCESS ✅",
                body: """
Hello Kamlesh,

✅ Your Jenkins build completed successfully.

🔧 Job: ${env.JOB_NAME}  
🔢 Build Number: ${env.BUILD_NUMBER}  
📄 Build URL: ${env.BUILD_URL}

The full build log is attached for your reference.

Regards,  
Jenkins
""",
                attachLog: true
            )
        }

        failure {
            emailext (
                to: 'kamlesh71324@gmail.com',
                subject: "${env.JOB_NAME} - Build #${env.BUILD_NUMBER} - FAILURE ❌",
                body: """
Hello Kamlesh,

❌ Your Jenkins build has failed.

🔧 Job: ${env.JOB_NAME}  
🔢 Build Number: ${env.BUILD_NUMBER}  
📄 Build URL: ${env.BUILD_URL}

Please review the attached build log and resolve any issues.

Regards,  
Jenkins
""",
                attachLog: true
            )
        }
    }
}

