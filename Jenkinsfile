pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps{
                sh 'git checkout ${BRANCH_NAME}'
            }
        }
        stage('Release') {
            when { branch 'master' }
            environment {
                DOCKER_REPOSITORY = 'isiachi'
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