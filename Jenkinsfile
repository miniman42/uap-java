pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Update Core') { 
 	    agent {
                docker { image 'git:alpine' }
            }            
	    steps {
                sh 'git submodule update --init --remote --checkout --recursive' 
            }
        }:
        stage('Package') {
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
