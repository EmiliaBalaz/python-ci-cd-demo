pipeline {
    agent any

    stages {
        stage('Clone repo') {
            steps {
                git 'https://github.com/tvoj-username/python-ci-cd-demo.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run tests') {
            steps {
                sh 'pytest'
            }
        }
    }
}
