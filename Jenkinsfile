pipeline {
    agent any

    environment {
        GIT_CREDENTIALS_ID = 'b1827b74-9fe0-4e02-b4a4-6eb894226e9c'  // Replace with your actual credentials ID in Jenkins
        REPO_URL = 'https://github.com/ShrivaThshaN/Tourism-Recommendation-Platform.git'
        BRANCH_NAME = 'main'  // Change if using a different branch
    }

    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: "*/${BRANCH_NAME}"]],
                        userRemoteConfigs: [[
                            url: REPO_URL,
                            credentialsId: GIT_CREDENTIALS_ID
                        ]]
                    ])
                }
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                script {
                    dir('frontend') {
                        sh 'npm install'
                    }
                }
            }
        }

        stage('Run Frontend Tests') {
            steps {
                script {
                    dir('frontend') {
                        sh 'npm test'
                    }
                }
            }
        }

        stage('Build Frontend') {
            steps {
                script {
                    dir('frontend') {
                        sh 'npm run build'
                    }
                }
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                script {
                    dir('backend') {
                        sh 'pip install -r requirements.txt'
                    }
                }
            }
        }

        stage('Run Backend Tests') {
            steps {
                script {
                    dir('backend') {
                        sh 'pytest'  // Adjust if using a different test framework
                    }
                }
            }
        }

        stage('Start Backend Server') {
            steps {
                script {
                    dir('backend') {
                        sh 'python app.py &'  // Adjust based on your backend setup
                    }
                }
            }
        }

        stage('Start Frontend') {
            steps {
                script {
                    dir('frontend') {
                        sh 'npm start &'  // Adjust if using a different command
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
