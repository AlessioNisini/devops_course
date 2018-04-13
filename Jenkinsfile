pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('release') {
            when {branch 'master'}
            environment {
                DOCKER_REPOSITORY = 'alessionisini'
            }
            steps {
                sh 'sbt release'
            }
        }
    }
}