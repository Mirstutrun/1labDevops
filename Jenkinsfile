pipeline {
    agent any
    stages {
        stage('Install') {
            steps {
                bat 'python -m venv venv'
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