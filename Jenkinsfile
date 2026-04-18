pipeline {
    agent any

    environment {
        IMAGE_NAME = "api-calculadora"
        CONTAINER_NAME = "api-calculadora-container"
    }

    stages {

        stage('Clonar repositorio') {
            steps {
                git branch: 'main',
                url: 'https://github.com/titolujanh/api_calculadora.git'
            }
        }

        stage('Verificar Python') {
            steps {
                sh 'python3 --version || python --version'
            }
        }

        stage('Instalar dependencias') {
            steps {
                sh 'pip install --upgrade pip'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Ejecutar tests (opcional)') {
            steps {
                sh 'python -m unittest discover || true'
            }
        }

        stage('Construir imagen Docker') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Detener contenedor anterior') {
            steps {
                sh 'docker stop $CONTAINER_NAME || true'
                sh 'docker rm $CONTAINER_NAME || true'
            }
        }

        stage('Ejecutar contenedor') {
            steps {
                sh 'docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline ejecutado correctamente'
        }
        failure {
            echo '❌ Error en el pipeline'
        }
    }
}