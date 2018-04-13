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
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USER', passwordVariable: 'PSW')]) {
                    sh 'docker login -u ${USER} -p ${PSW}'
                }
                sshagent (credentials: ['GitHub']) {
                    sh 'sbt "release with-defaults"'
                }
            }
        }
    }
    post {
        always {
            deleteDir()
        }
    }
}