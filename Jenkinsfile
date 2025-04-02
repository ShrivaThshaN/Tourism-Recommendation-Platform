pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/aadhil2k4/Tourism-Recommendation-Platform.git'
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir('frontend') {
                    sh 'npm install'
                }
            }
        }

        stage('Run Frontend Tests') {
            steps {
                dir('frontend') {
                    sh 'npm test'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm run build'
                }
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('backend') {
                    sh 'npm install'
                }
            }
        }

        stage('Run Backend Tests') {
            steps {
                dir('backend') {
                    sh 'npm test'
                }
            }
        }

        stage('Start Backend Server') {
            steps {
                dir('backend') {
                    sh 'npm start &'
                }
            }
        }

        stage('Start Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm run dev'
                }
            }
        }
    }
}
