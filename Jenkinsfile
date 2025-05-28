pipeline {
    agent any
    
    environment {
        DIRECTORY_PATH = "/var/jenkins_home"
        TESTING_ENVIRONMENT = "TASK_6.1C"
        PRODUCTION_ENVIRONMENT = "Akashdeep Singh Sidhu"
        EMAIL_RECIPIENT = "kamlesh71324@gmail.com"
    }
    
    stages {
        stage('Build') {
            steps {
                script {
                    echo "Getting source code from: $DIRECTORY_PATH"
                    echo "Building the code using Maven..."
                    echo "Tool used: Maven"
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo "Running Unit tests using JUnit.."
                    echo "Running Integration tests using Selenium..."
                    echo "Tools used: JUnit, Selenium"
                }
            }
            post {
                success {
                    emailext to: "$EMAIL_RECIPIENT",
                        subject: "Unit and Integration Tests: SUCCESS",
                        body: "The Unit and Integration tests have passed.",
                        attachLog: true
                }
                failure {
                    emailext to: "$EMAIL_RECIPIENT",
                        subject: "Unit and Integration Tests: FAILURE",
                        body: "The Unit and Integration tests have failed.",
                        attachLog: true
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                script {
                    echo "Performing code analysis using SonarQube.."
                    echo "Tool used: SonarQube"
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                script {
                    echo "Performing security scan using OWASP Dependency-Check.."
                    echo "Tool used: OWASP Dependency-Check"
                }
            }
            post {
                success {
                    emailext to: "$EMAIL_RECIPIENT",
                        subject: "Security Scan: SUCCESS",
                        body: "The security scan has passed.",
                        attachLog: true
                }
                failure {
                    emailext to: "$EMAIL_RECIPIENT",
                        subject: "Security Scan: FAILURE",
                        body: "The security scan has failed.",
                        attachLog: true
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    echo "Deploying the application to the staging environment: $TESTING_ENVIRONMENT"
                    echo "Staging server: AWS EC2 instance"
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo "Running Integration tests on the staging environment.."
                    echo "Tools used: Selenium"
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    echo "Deploying the application to the production environment: $PRODUCTION_ENVIRONMENT"
                    echo "Production server: AWS EC2 instance"
                }
            }
        }
    }
    
    post {
        always {
            echo "Pipeline execution completed"
        }
        success {
            echo "Pipeline executed successfully"
            emailext to: "$EMAIL_RECIPIENT",
                subject: "Build Status: SUCCESS",
                body: "The Jenkins pipeline has successfully completed all stages.",
                attachLog: true
        }
        failure {
            echo "Pipeline execution failed"
            emailext to: "$EMAIL_RECIPIENT",
                subject: "Build Status: FAILURE",
                body: "The Jenkins pipeline has failed.",
                attachLog: true
        }
    }
}
