pipeline {
    agent {
        docker {
            image 'node:18'  // Updated to Node.js 18
            args '-u root'
        }
    }
    environment {
        NODE_ENV = "production"
    }
    stages {
        stage('Checkout') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    git url: 'https://github.com/shyam9307/Restaurent_Application', branch: 'main'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    sh 'npm install'
                    sh 'npm install -g @angular/cli'
                }
            }
        }
        stage('Build') {
            steps {
                timeout(time: 10, unit: 'MINUTES') {
                    sh 'ng version'  // Check Angular CLI and Node.js version before build
                    sh 'ng build'
                }
            }
        }
        stage('Test') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    sh 'npm test'
                }
            }
        }
        stage('Archive Artifacts') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    archiveArtifacts artifacts: 'dist/**', fingerprint: true
                }
            }
        }
    }
    post {
        success {
            echo "✅ Build and tests completed successfully!"
        }
        failure {
            echo "❌ Build failed. Please check the console output for errors."
        }
    }
}
