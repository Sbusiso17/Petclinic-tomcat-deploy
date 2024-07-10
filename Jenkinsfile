@Library('jenkins-lib') _
pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                gitCheckout()
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
                script {
                    def adminName = "Sbongokuhle"  
                    
                    def userInput = input(
                        id: 'Proceed1', 
                        message: 'Deploy to production?', 
                        parameters: [
                            string(defaultValue: '', description: 'Enter admin name for approval', name: 'ADMIN_NAME'),
                            booleanParam(defaultValue: true, description: 'Check to proceed with deployment', name: 'APPROVE_DEPLOYMENT')
                        ]
                    )
                    
                    if (userInput.ADMIN_NAME == adminName && userInput.APPROVE_DEPLOYMENT) {
                        echo "Deployment approved by admin: ${userInput.ADMIN_NAME}"
                    } else if (userInput.ADMIN_NAME != adminName) {
                        error "Deployment rejected. Invalid admin name provided."
                    } else {
                        error "Deployment aborted by user."
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the .war file into a tomcat prod server"
                sshagent(['tomcat-pipeline']) {
                    sh "scp -o StrictHostKeyChecking=no target/petclinic.war tomcat@100.26.191.108:/opt/tomcat/webapps "
                }
            }
        }    
    }
}
