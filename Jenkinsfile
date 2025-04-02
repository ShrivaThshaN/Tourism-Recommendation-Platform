pipeline {
    agent any

    environment {
        NODEJS_HOME = "C:\\Program Files\\nodejs"
        PATH = "${NODEJS_HOME};${PATH}"
    }

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/ShrivaThshaN/Tourism-Recommendation-Platform.git'
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir('frontend') {
                    bat 'npm install'
                }
            }
        }

        stage('Run Frontend Tests') {
            steps {
                dir('frontend') {
                    bat 'npx vitest'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    bat 'npm run build'
                }
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('backend') {
                    bat 'npm install'
                }
            }
        }

        stage('Run Backend Tests') {
            steps {
                dir('backend') {
                    bat 'npm test'
                }
            }
        }

        stage('Start Backend Server') {
            steps {
                dir('backend') {
                    bat 'npm start'
                }
            }
        }

        stage('Start Frontend') {
            steps {
                dir('frontend') {
                    bat 'npm start'
                }
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
        success {
            echo 'Pipeline executed successfully!'
        }
    }
}
