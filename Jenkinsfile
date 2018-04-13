pipeline {
    agent any
    stages {
        stage('Branch checkout') {
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