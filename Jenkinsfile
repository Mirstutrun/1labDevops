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
        stage('Merge to master') {
            when { expression { env.GIT_BRANCH == 'origin/dev' } }
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-token',
                                 usernameVariable: 'GH_USER', passwordVariable: 'GH_TOKEN')]) {
                    bat '''
                        git config user.email "jenkins@local"
                        git config user.name "Jenkins"
                        git fetch origin master
                        git checkout -B master origin/master
                        git merge --no-ff origin/dev -m "Auto-merge dev into master (tests passed)"
                        git push https://%GH_USER%:%GH_TOKEN%@github.com/Mirstutrun/1labDevops.git master
                    '''
                }
            }
        }
    }
}