pipeline {

    agent any

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
                echo 'Application Build Successful'
            }
        }
        stage('Archive') {
             steps {
            archiveArtifacts artifacts: '**/*', fingerprint: true
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