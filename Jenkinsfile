pipeline {
    agent { label 'slave1' } 
    stages {
        stage('checkout1') {
                steps {
                sh "rm -rf /home/slave1/workspace/jfrogpipe/hello-world-war"
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
                                 ] 
                                 }'''
                          )
                  }
       }
        stage('Copy to Tomcat') {
            steps {
                // Copy files to the Tomcat webapps directory
                sh "cp /home/slave1/workspace/jfrogpipe/target/hello-world-war-1.0.1.war /opt/apache-tomcat-8.5.90/webapps/"
                // setting permission to /bin/shutdown.sh and /bin/startup.sh
                sh 'chmod 777 /opt/apache-tomcat-8.5.90/bin/shutdown.sh'
                sh 'chmod 777 /opt/apache-tomcat-8.5.90/bin/startup.sh'
                // Restart Tomcat (if required)
                sh '/opt/apache-tomcat-8.5.90/bin/shutdown.sh'
                sh '/opt/apache-tomcat-8.5.90/bin/startup.sh'
            }
        }              
            }	
       }
    

