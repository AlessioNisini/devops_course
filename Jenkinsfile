pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                sh 'git checkout ${BRANCH_NAME}'
            }
        }
        stage('release') {
            when {branch 'master'}
            environment {
                DOCKER_REPOSITORY = 'alessionisini'
            }
            steps {
                sh 'sbt "release with-defaults"'
            }
        }
    }
    post {
        always {
            deleteDir()
        }
    }
}