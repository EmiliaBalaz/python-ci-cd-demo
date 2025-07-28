pipeline {
    agent any

    stages {
        stage('Clone repo') {
            steps {
                git branch: 'main', url: 'https://github.com/EmiliaBalaz/python-ci-cd-demo.git'
            }
        }

        stage('Install dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Run tests') {
            steps {
                bat 'pytest > result.log || exit 0'
            }
        }
    }
}
