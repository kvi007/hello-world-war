pipeline {
    agent { label 'slave1' } 
    stages {
        stage('checkout1') {
                steps {
                sh 'rm -rf /home/slave1/workspace/jfrogpipe/hello-world-war'
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
                        )
            stage('Deploy to Tomcat') {
              steps {
        // Copy the WAR file to the Tomcat webapps directory
                            sh "cp /home/slave1/workspace/jfrogpipe/target/hello-world-war-1.0.1 /opt/apache-tomcat-8.5.90/webapps/"

        // Restart Tomcat to deploy the application
                            sh 'service tomcat restart'
                          }
                    }                      
            }	
       }
    }
}
