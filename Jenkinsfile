pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                echo "checking out at our code"
                git branch: 'main', url: 'https://github.com/Sbusiso17/Petclinic-tomcat-deploy.git'
            }
        }
         stage('Compile') {
            steps {
                echo "compiling our code"
               sh "mvn clean compile"
            }
        }
        stage('Validate') {
            steps {
                echo "running validation on maven build"
               sh "mvn clean validate"
            }
        }
        stage('Test') {
            steps {
                echo "running test on maven build"
               sh "mvn clean test"
            }
        }
     stage('Build') {
            steps {
                echo "packaging the project into a .war file"
               sh "mvn clean install"
            }
        }
    stage('Deploy') {
            steps {
                 echo "Deploying the .war file into a tomcat prod server"
            sshagent(['tomcat-pipeline']) {
                  sh "scp -o StrictHostKeyChecking=no target/petclinic.war tomcat@3.83.107.27:/opt/tomcat/webapps "
               }
            }
        }    
    }
}
           
       
