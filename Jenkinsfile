pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }
        stage('Test in Parallel') {
            parallel {
                stage('ls Tests') {
                    steps {
                        echo 'Running ls tests...'
                        sh 'ls -l'
                    }
                }
                stage('Unit Tests') {
                    steps {
                        echo 'Running unit tests...'
                        sh 'sleep 5'
                    }
                }
                stage('Integration Tests') {
                    steps {
                        echo 'Running integration tests...'
                        sh 'sleep 5'
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
    stage('Deploy') {
        when {
            input "Do you want to proceed with deployment?"
        }
        steps {
            echo 'Deploying application...'
        }
    }
    }
    post {
        success {
            echo 'Pipeline completed successfully 🎉'
        }
        failure {
            echo 'Pipeline failed ❌'
        }
}
}
