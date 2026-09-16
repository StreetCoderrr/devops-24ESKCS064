pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Environment') {
            steps {
                bat '"C:\\Users\\aryan\\AppData\\Local\\Python\\bin\\python.exe" --version'
            }
        }

        stage('Create Virtual Environment') {
            steps {
                bat '"C:\\Users\\aryan\\AppData\\Local\\Python\\bin\\python.exe" -m venv .jenkins-venv'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '.jenkins-venv\\Scripts\\python.exe -m pip install --upgrade pip'
                bat '.jenkins-venv\\Scripts\\python.exe -m pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                bat '.jenkins-venv\\Scripts\\python.exe -m pytest -v'
            }
        }

        stage('Verify Project') {
            steps {
                bat 'if not exist app.py exit /b 1'
                bat 'if not exist predict.py exit /b 1'
                bat 'if not exist requirements.txt exit /b 1'
                bat 'if not exist tests exit /b 1'
                bat 'if not exist models exit /b 1'

                echo 'AirQualityPrediction project verification successful.'
            }
        }
    }

    post {
        success {
            echo 'AirQualityPrediction Jenkins pipeline completed successfully.'
        }

        failure {
            echo 'AirQualityPrediction Jenkins pipeline failed.'
        }

        always {
            echo 'Jenkins build finished.'
        }
    }
}