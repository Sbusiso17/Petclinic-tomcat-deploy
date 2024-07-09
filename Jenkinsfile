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
        stage('Approval') {
            steps {
<<<<<<< HEAD
            
=======
                script {
                    def userInput = input(id: 'Proceed1', message: 'Deploy to production?', parameters: [
                        [$class: 'BooleanParameterDefinition', defaultValue: true, description: 'Check to proceed with deployment', name: 'Please confirm deployment']
                    ])
                    
                    if(userInput == true) {
                        echo "User approved the deployment"
                    } else {
                        error "User aborted the deployment"
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the .war file into a tomcat prod server"
                sshagent(['tomcat-pipeline']) {
                    sh "scp -o StrictHostKeyChecking=no target/petclinic.war tomcat@54.152.252.127:/opt/tomcat/webapps "
                }
>>>>>>> adb98aa (adding the aproval stage to our pipeline)
            }
        }    
    }
}
