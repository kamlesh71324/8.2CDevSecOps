pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                // Simulate a failure to test email
                sh 'exit 1'
            }
        }
    }

    post {
        always {
            script {
                emailext (
                    subject: "Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                    body: """
                        <p>Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]': ${currentBuild.currentResult}</p>
                        <p>Check console output at <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                    """,
                    mimeType: 'text/html',
                    attachLog: true,
                    to: 'kamlesh71324@gmail.com'
                )
            }
        }
    }
}


