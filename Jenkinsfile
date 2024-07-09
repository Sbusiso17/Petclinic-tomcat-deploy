pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/writetoritika/Petclinic.git'
            }
        }
     stage('Build') {
            steps {
               sh "mvn clean install"
            }
        }
    stage('Deploy') {
            steps {
            sshagent(['tomcat-pipeline']) {
                  sh "scp -o StrictHostKeyChecking=no target/petclinic.war tomcat@3.83.107.27/:/opt/tomcat/webapps "
               }
            }
        }    
    }
}
           
       
