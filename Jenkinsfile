pipeline {
    agent any

    environment {
        NODEJS_HOME = tool 'NodeJS 18+'  // Ensure this matches the Jenkins tool name
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/patildinu/Restaurent_Application.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'ng build --configuration production'
            }
        }

        stage('Test') {
            steps {
                sh 'ng test --watch=false --browsers=ChromeHeadless'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Application...'
                // Add deployment steps here (e.g., AWS S3, Firebase, Nginx, etc.)
            }
        }
    }
}





// Old code

// pipeline {
//     agent any

//     environment {
//         NODE_HOME = 'C:\\Program Files\\nodejs'
//         PATH = "${NODE_HOME};${env.PATH}"
//     }

//     stages {
//         stage('Checkout Code') {
//     steps {
//         git branch: 'main', url: 'https://github.com/patildinu/Restaurent_Application.git'
//     }
// }

//         stage('Install Dependencies') {
//     steps {
//         bat 'npm install'
//     }
// }


//         stage('Build Angular Project') {
//             steps {
//                 sh 'npm run build -- --configuration=production'
//             }
//         }

//         stage('Run Unit Tests') {
//             steps {
//                 sh 'npm test -- --watch=false --browsers=ChromeHeadless'
//             }
//         }

//         stage('Publish Test Reports') {
//             steps {
//                 script {
//                     publishHTML([
//                         reportDir: 'coverage',
//                         reportFiles: 'index.html',
//                         reportName: 'Test Report',
//                         allowMissing: true,
//                         alwaysLinkToLastBuild: true,
//                         keepAll: true
//                     ])
//                 }
//             }
//         }

//         stage('Archive Build Artifacts') {
//             steps {
//                 archiveArtifacts artifacts: 'dist/**', fingerprint: true
//             }
//         }

//         stage('Deploy') {
//             steps {
//                 echo 'Deploying the application...'
//                 // **Add deployment commands here**
//                 // Example: Copy built files to a server using SCP or FTP
//                 // sh 'scp -r dist/your-angular-app/* user@your-server:/var/www/html/'
//             }
//         }
//     }

//     post {
//         success {
//             echo '✅ Build and Deployment Successful 🎉'
//         }
//         failure {
//             echo '❌ Build Failed, Check Logs!'
//         }
//     }
// }
