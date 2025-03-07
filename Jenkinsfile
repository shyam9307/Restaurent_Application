// pipeline {
//     agent any

//     environment {
//         NODE_HOME = tool name: 'NodeJS_18', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
//         PATH = "${NODE_HOME}/bin:${env.PATH}"
//     }

//     stages {
//         stage('Checkout Code') {
//             steps {
//                 git 'https://github.com/patildinu/Restaurent_Application.git'
//             }
//         }
//         stage('Install Dependencies') {
//             steps {
//                 sh 'npm install'
//             }
//         }
//         stage('Build Angular Project') {
//             steps {
//                 sh 'npm run build -- --configuration=production'
//             }
//         }
//         stage('Run Tests') {
//             steps {
//                 sh 'npm test -- --watch=false --browsers=ChromeHeadless'
//             }
//         }
//         stage('Publish Test Reports') {
//             steps {
//                 publishHTML([allowMissing: true, alwaysLinkToLastBuild: true, keepAll: true, reportDir: 'coverage', reportFiles: 'index.html', reportName: 'Test Report'])
//             }
//         }
//         stage('Deploy (Optional)') {
//             steps {
//                 echo 'Deploying the application...'
//                 // Add deployment commands here (e.g., FTP, SSH, or Firebase Hosting)
//             }
//         }
//     }
// }



pipeline {
    agent any

    environment {
        NODE_HOME = 'C:\\Program Files\\nodejs'
        PATH = "${NODE_HOME};${env.PATH}"
    }

    stages {
        stage('Checkout Code') {
    steps {
        git branch: 'main', url: 'https://github.com/patildinu/Restaurent_Application.git'
    }
}

        stage('Install Dependencies') {
    steps {
        bat 'npm install'
    }
}


        stage('Build Angular Project') {
            steps {
                sh 'npm run build -- --configuration=production'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'npm test -- --watch=false --browsers=ChromeHeadless'
            }
        }

        stage('Publish Test Reports') {
            steps {
                script {
                    publishHTML([
                        reportDir: 'coverage',
                        reportFiles: 'index.html',
                        reportName: 'Test Report',
                        allowMissing: true,
                        alwaysLinkToLastBuild: true,
                        keepAll: true
                    ])
                }
            }
        }

        stage('Archive Build Artifacts') {
            steps {
                archiveArtifacts artifacts: 'dist/**', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // **Add deployment commands here**
                // Example: Copy built files to a server using SCP or FTP
                // sh 'scp -r dist/your-angular-app/* user@your-server:/var/www/html/'
            }
        }
    }

    post {
        success {
            echo '✅ Build and Deployment Successful 🎉'
        }
        failure {
            echo '❌ Build Failed, Check Logs!'
        }
    }
}
