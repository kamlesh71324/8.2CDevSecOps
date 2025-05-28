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
    

    post {
        always {
            emailext(
                to: 'kamlesh71324@gmail.com',
                subject: "${env.JOB_NAME} - Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                body: """
Hello Kamlesh,

Your Jenkins build has completed.

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Status: ${currentBuild.currentResult}

You can also view the build log here: ${env.BUILD_URL}

Thanks,
Jenkins
                """,
                attachLog: true
            )
        }
    }
}
