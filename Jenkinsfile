pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps{
                checkout scm
            }
        }
        stage('Release') {
            when { branch 'master' }
            environment {
                DOCKER_REPOSITORY = 'isiachi'
            }
            steps {
                sh 'sbt release'
            }
        }
    }
}