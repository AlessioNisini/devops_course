pipeline {
    agent any
    stages {
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