pipeline {
    agent none
    stages {
        stage('Update Core') {
            agent {
                docker { image 'alpine/git' }
            }
            steps {
                sh 'git submodule update --init --remote --checkout --recursive'
            }
        }
        stage('Package') {
            agent {
                docker {
                    image 'maven:3-alpine'
                    args '-v /root/.m2:/root/.m2'
                }
            }
            steps {
                sh 'mvn package'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }
}
