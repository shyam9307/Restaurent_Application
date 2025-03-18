pipeline {
    agent {
        docker {
            image 'node:16'  // Using Node.js 16 for better compatibility
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
                            sh 'echo "🔄 Setting NPM legacy-peer-deps..."'
                            sh 'npm config set legacy-peer-deps true'

                            sh 'echo "🔄 Running npm install"'
                            sh 'npm install'  // Handles dependency conflicts

                            sh 'echo "🔄 Installing Angular CLI globally"'
                            sh 'npm install -g @angular/cli'

                            sh 'echo "🔄 Verifying Angular CLI installation"'
                            sh 'npx ng version'  // Check Angular CLI availability
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
                    sh 'echo "🔍 Checking Angular CLI version"'
                    sh 'npx ng version'  // Ensure CLI is accessible

                    sh 'echo "🔄 Running ng build"'
                    sh 'npx ng build'  // Use npx to execute Angular CLI
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
                // Add deployment commands here
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








// pipeline {
//     agent {
//         docker {
//             image 'node:18.19.0'  // Using Node.js 18.19
//             args '-u root'
//         }
//     }
//     environment {
//         NODE_ENV = "production"
//         CI = 'false'  // Disables CI mode for npm
//     }
//     stages {
//         stage('Checkout') {
//             steps {
//                 echo "🔄 Starting Checkout stage..."
//                 timeout(time: 2, unit: 'MINUTES') {
//                     git url: 'https://github.com/shyam9307/Restaurent_Application', branch: 'main'
//                 }
//                 echo "✅ Checkout completed!"
//             }
//         }
        
//         stage('Install Dependencies') {
//             steps {
//                 echo "📦 Installing Dependencies..."
//                 timeout(time: 5, unit: 'MINUTES') {
//                     script {
//                         try {
//                             sh 'echo "🔄 Running npm install --legacy-peer-deps"'
//                             sh 'npm install --legacy-peer-deps'  // Handles dependency conflicts

//                             sh 'echo "🔄 Installing Angular CLI globally"'
//                             sh 'npm install -g @angular/cli'
//                         } catch (Exception e) {
//                             echo '⚠️ npm install failed, retrying with --force'
//                             sh 'npm install --force'
//                         }
//                     }
//                 }
//                 echo "✅ Dependencies installed successfully!"
//             }
//         }

//         stage('Check Node Version') {
//            steps {
//                echo "🔍 Checking Node.js and npm versions..."
//                sh 'node -v'
//                sh 'npm -v'
//                echo "✅ Node.js and npm versions verified!"
//            }
//         }
      
//         stage('Build') {
//             steps {
//                 echo "🏗️ Starting Build process..."
//                 timeout(time: 10, unit: 'MINUTES') {
//                     sh 'echo "🔍 Checking Angular CLI version"'
//                     sh 'ng version'  // Check Angular CLI and Node.js version before build

//                     sh 'echo "🔄 Running ng build"'
//                     sh 'ng build'
//                 }
//                 echo "✅ Build completed successfully!"
//             }
//         }
        
//         stage('Test') {
//             steps {
//                 echo "🧪 Running Tests..."
//                 timeout(time: 5, unit: 'MINUTES') {
//                     sh 'npm test'
//                 }
//                 echo "✅ Tests completed!"
//             }
//         }
        
//         stage('Archive Artifacts') {
//             steps {
//                 echo "📦 Archiving Build Artifacts..."
//                 timeout(time: 2, unit: 'MINUTES') {
//                     archiveArtifacts artifacts: 'dist/**', fingerprint: true
//                 }
//                 echo "✅ Artifacts archived!"
//             }
//         }
        
//         stage('Deploy') {
//             steps {
//                 echo "🚀 Starting Deployment..."
//                 // Add deployment commands here
//                 echo "✅ Deployment process completed!"
//             }
//         }
//     }
    
//     post {
//         success {
//             echo "🎉✅ Build and tests completed successfully!"
//         }
//         failure {
//             echo "❌ Build failed. Please check the console output for errors."
//         }
//     }
// }
