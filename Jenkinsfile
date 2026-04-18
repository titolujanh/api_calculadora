pipeline {
    agent any

    stages {

        stage('Build Docker') {
            steps {
                sh 'docker build -t api-calculadora .'
            }
        }

        stage('Run API') {
            steps {
                sh '''
                    docker stop api || true
                    docker rm api || true
                    docker run -d -p 5000:5000 --name api api-calculadora
                '''
            }
        }
    }
}