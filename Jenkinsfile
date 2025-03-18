pipeline {
    agent {
        docker {
            image 'node:16'
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
                    // Clone the repository from GitHub
                    git url: 'https://github.com/shyam9307/Restaurent_Application', branch: 'main'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                timeout(time: 7, unit: 'MINUTES') {
                    // Install npm dependencies
                    sh 'npm install'
                    // Install Angular CLI globally so that 'ng' command is available
                    sh 'npm install -g @angular/cli'
                }
            }
        }
        stage('Build') {
            steps {
                timeout(time: 10, unit: 'MINUTES') {
                    // Build the Angular application
                    sh 'ng build'
                }
            }
        }
        stage('Test') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    // Run tests if defined in package.json
                    sh 'npm test'
                }
            }
        }
        stage('Archive Artifacts') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    // Archive the build artifacts (assuming output is in the "dist" directory)
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
