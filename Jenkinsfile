pipeline {
    agent { label 'slave1' } 
    stages {
        stage('checkout') {
            steps {
                sh 'git clone https://github.com/KiranVItagi/hello-world-war'
            }
        }
           stage('build') {
            steps {
                sh 'mvn package'
            }
        }
           }
    }
