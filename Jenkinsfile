pipeline {
    agent {
        docker {
        image 'node:6-alpine'
        args  '-p 3000:3000'
    }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input 'Deploy para ambiente de desenvolvimento?'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deliver for production') {
            when {
                branch 'production'
            }
            steps {
                sh './jenkins/scripts/deliver-for-production.sh'
                input 'Deploy para ambiente de producao?'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }

}
