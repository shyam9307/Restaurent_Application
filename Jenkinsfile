pipeline {
    agent {
        docker {
            image 'node:16'  // Using Node.js 16 (Angular 12 supports Node 16)
            args '-u root'
        }
    }
    environment {
        NODE_ENV = "production"
        CI = 'false'  // Disables CI mode for npm
    }
    stages {
        stage('Checkout') {
            steps {
                echo "🔄 Starting Checkout stage..."
                timeout(time: 2, unit: 'MINUTES') {
                    git url: 'https://github.com/shyam9307/Restaurent_Application', branch: 'main'
                }
                echo "✅ Checkout completed!"
            }
        }
        
        stage('Install Dependencies') {
            steps {
                echo "📦 Installing Dependencies..."
                timeout(time: 5, unit: 'MINUTES') {
                    script {
                        try {
                            echo "🔄 Setting NPM legacy-peer-deps..."
                            sh 'npm config set legacy-peer-deps true'
                            
                            echo "🔄 Running npm install..."
                            sh 'npm install'
                            
                            echo "🔄 Installing Angular CLI globally (v12.2.10)..."
                            sh 'npm install -g @angular/cli@12.2.10'
                            
                            echo "🔄 Installing @angular-devkit/build-angular locally..."
                            sh 'npm install --save-dev @angular-devkit/build-angular'
                            
                            echo "🔄 Verifying Angular CLI installation..."
                            sh 'npx ng version'
                        } catch (Exception e) {
                            echo '⚠️ npm install failed, retrying with --force'
                            sh 'npm install --force'
                        }
                    }
                }
                echo "✅ Dependencies installed successfully!"
            }
        }
        
        stage('Check Node Version') {
           steps {
               echo "🔍 Checking Node.js and npm versions..."
               sh 'node -v'
               sh 'npm -v'
               echo "✅ Node.js and npm versions verified!"
           }
        }
      
        stage('Build') {
            steps {
                echo "🏗️ Starting Build process..."
                timeout(time: 10, unit: 'MINUTES') {
                    echo "🔍 Checking Angular CLI version before build..."
                    sh 'npx ng version'
                    
                    echo "🔄 Running ng build..."
                    sh 'npx ng build'
                }
                echo "✅ Build completed successfully!"
            }
        }
        
        stage('Test') {
            steps {
                echo "🧪 Running Tests..."
                timeout(time: 5, unit: 'MINUTES') {
                    sh 'npm test'
                }
                echo "✅ Tests completed!"
            }
        }
        
        stage('Archive Artifacts') {
            steps {
                echo "📦 Archiving Build Artifacts..."
                timeout(time: 2, unit: 'MINUTES') {
                    archiveArtifacts artifacts: 'dist/**', fingerprint: true
                }
                echo "✅ Artifacts archived!"
            }
        }
        
        stage('Deploy') {
            steps {
                echo "🚀 Starting Deployment..."
                // Add your deployment commands here if needed
                echo "✅ Deployment process completed!"
            }
        }
    }
    
    post {
        success {
            echo "🎉✅ Build and tests completed successfully!"
        }
        failure {
            echo "❌ Build failed. Please check the console output for errors."
        }
    }
}
