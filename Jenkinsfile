pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js dependencies...'
                sh 'npm ci'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application...'
                sh 'node --check server.js'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Restarting LIC Portal service...'
                sh 'sudo systemctl restart lic-portal'
            }
        }

        stage('Verify') {
            steps {
                echo 'Checking LIC Portal service...'
                sh 'sudo systemctl is-active lic-portal'
                sh 'curl -f http://localhost:3000'
            }
        }
    }

    post {
        success {
            echo 'LIC Portal deployment successful!'
        }

        failure {
            echo 'LIC Portal deployment failed!'
        }
    }
}
