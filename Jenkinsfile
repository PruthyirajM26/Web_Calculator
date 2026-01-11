pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/PruthyirajM26/Web_Calculator.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t web-calculator .
                '''
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop web-calculator || true
                docker rm web-calculator || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker run -d \
                --name web-calculator \
                -p 8080:8080 \
                web-calculator
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Web Calculator deployed successfully"
        }
        failure {
            echo "❌ Pipeline failed"
        }
    }
}