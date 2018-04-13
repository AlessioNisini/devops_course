pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
                sh 'git checkout ${env.BRANCH_NAME}'
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