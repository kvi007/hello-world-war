pipeline {
    agent { label 'slave1' } 
    stages {
        stage('checkout1') {
            steps {
                sh rm -rf *
                sh 'git clone https://github.com/KiranVItagi/hello-world-war'
            }
        }
        stage('build') {
            steps {
                sh 'mvn package'
            }
        }
       stage('Push artifacts into artifactory') { 
           steps { 
               rtUpload ( 
                   serverId: 'kiranartifactory', 
                   spec:     '''{ 
                       "files": [ 
                           { 
                               "pattern": "*.war", 
                                "target": "example-repo-local/" 
                            }  
                            ] }'''
                        )	 }	}
    }
}
