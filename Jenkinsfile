pipeline {
    agent any
    parameters {
        choice(name: 'ENVIRONMENT', choices: ['dev', 'staging', 'prod'], description: 'Select deployment environment')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }
        stage('Test in Parallel') {
            parallel {
                stage('Linux Tests') {
                    steps {
                        echo 'Running tests on Linux environment...'
                        sh 'sleep 2'
                    }
                }
                stage('Windows Tests') {
                    steps {
                        echo 'Running tests on Windows environment...'
                        sh 'sleep 2'
                    }
                }
                stage('Unit Tests') {
                    when {
                        expression { currentBuild.currentResult == 'SUCCESS' }
                    }
                    steps {
                        echo 'Running unit tests...'
                        sh 'sleep 2'
                    }
                }
            }
        }
        stage('Archive Results') {
            steps {
                sh 'echo "All tests passed!" > results.txt'
                archiveArtifacts artifacts: 'results.txt', fingerprint: true
            }
        }
        stage('Approval') {
            options {
                timeout(time: 2, unit: 'MINUTES')
            }
            input {
                message "Do you want to proceed with deployment?"
            }
            steps {
                echo 'Deployment approved!'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying application to ${params.ENVIRONMENT} environment..."
            }
        }
    }
    post {
        success {
            echo '✅ Pipeline finished successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs!'
        }
        always {
            echo 'Pipeline completed (success or failure).'
        }
    }
}
