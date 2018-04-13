pipeline {
    agent any
    stages {
        stage('Branch checkout') {
            steps{
                sh 'git checkout ${BRANCH_NAME}'
            }
        }
        stage('Release') {
            when {allOf {branch 'master'; not {changeRequest author: 'Jenkins'}}}
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