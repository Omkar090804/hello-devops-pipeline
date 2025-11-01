pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Omkar090804/hello-devops-pipeline.git',
                    credentialsId: 'github-pat'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t hello-devops .'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    sh 'docker rm -f hello-container || true'
                    sh 'docker run -d -p 4000:3000 --name hello-container hello-devops'
                }
            }
        }
    }

    post {
        failure {
            echo '❌ Pipeline failed!'
        }
        success {
            echo '✅ Pipeline succeeded!'
        }
    }
}
