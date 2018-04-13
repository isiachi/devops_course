pipeline {
    agent any
    stages {
        stage('release') {
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