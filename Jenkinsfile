pipeline {

    agent any
   environment {
        APP_NAME = "simple-node-app"
        APP_VERSION = "1.0"
        ENVIRONMENT = "Development"
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Fix Permissions') {
            steps {
                sh 'chmod +x node_modules/.bin/jest'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                echo "Building ${APP_NAME}"
                echo "Version: ${APP_VERSION}"
                echo "Environment: ${ENVIRONMENT}"
                echo 'Application Build Successful'
            }
        }
        stage('Archive') {
             steps {
            archiveArtifacts artifacts: '**/*', fingerprint: true
         }
    
       stage('Deploy') {
            steps {
                sshagent(['ubuntu']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@16.170.169.199 << EOF

                    cd /home/ubuntu/simple-node-app

                    git pull origin main

                    npm install

                    pm2 restart simple-node-app

                    EOF
                    '''
                 }
            }
        }

    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}