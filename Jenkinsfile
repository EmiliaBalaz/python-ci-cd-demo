pipeline {
    agent any

    environment {
        SONARQUBE_ENV = credentials('general-token') 
    }

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
                bat 'pytest > result.log'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('server-sonar') {
                    bat '''
                        sonar-scanner ^
                        -Dsonar.projectKey=ci-cd-demo ^
                        -Dsonar.sources=. ^
                        -Dsonar.host.url=http://localhost:9000 ^
                        -Dsonar.login=sqp_6b4ad65d3889bc60be6b71a8995ba90f0f5e7dd0
                    '''
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
