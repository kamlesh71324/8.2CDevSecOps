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
                sh 'npm test || true'
            }
        }

        stage('Security Scan') {
            steps {
                sh 'npm audit || true'
            }
        }
    }

    // Test auto-trigger 2
    post {
    always {
        mail to: 'kamlesh71324@gmail.com',
             subject: "${env.JOB_NAME} - Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
             body: """Hello Kamlesh,

Your Jenkins build has finished.

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Status: ${currentBuild.currentResult}

View the full build log here: ${env.BUILD_URL}

Thanks,
Jenkins"""
    }
}
}
