pipeline {
    agent {
        docker {
            image 'node:16'
            args '-u root'
        }
    }
    environment {
        // Set any environment variables if needed (e.g., NODE_ENV)
        NODE_ENV = "production"
    }
    stages {
        stage('Checkout') {
            steps {
                // Cloning the repository from GitHub
                git url: 'https://github.com/shyam9307/Restaurent_Application', branch: 'main'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Install project dependencies using npm
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                // Build the project; change this command if your package.json uses a different build command.
                // For Angular projects, you might use: ng build --prod
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                // Run tests defined in your package.json (if available)
                sh 'npm test'
            }
        }
        stage('Archive Artifacts') {
            steps {
                // Archive the build artifacts (adjust the path to your actual output folder)
                archiveArtifacts artifacts: 'dist/**', fingerprint: true
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
