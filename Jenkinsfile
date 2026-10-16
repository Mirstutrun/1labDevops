pipeline {
    agent any
    environment {
        PYTHON = 'C:\\Users\\Alex\\AppData\\Local\\Python\\bin\\python.exe'
    }
    stages {
        stage('Install') {
            steps {
                bat '"%PYTHON%" -m venv venv'
                bat 'venv\\Scripts\\pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                bat 'venv\\Scripts\\python -m pytest -v'
            }
        }
    }
}