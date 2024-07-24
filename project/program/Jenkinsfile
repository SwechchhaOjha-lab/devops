pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/user/repo.git'
        BRANCH = 'main'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                sh 'docker build -t myapp .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'docker run --rm myapp pytest tests/'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sshagent(['deploy-key']) {
                    sh 'scp -o StrictHostKeyChecking=no myapp.tar.gz user@server:/path/to/deploy'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

