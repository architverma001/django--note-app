@Library("Shared") _
pipeline {
    agent {label "agent"}

    stages {
        stage("hello"){
            steps{
               script {
                   hello()
               }        
            }
        }
        
        
        
        stage('cloning the code') {
            steps {
              script{
                  clone("https://github.com/architverma001/django--note-app","main")
              }
            }
        }
        
        stage('Build') {
            steps {
               echo "Building project"
               sh "docker build -t notes-app:latest ."
            }
        }
        
        stage('testing the code') {
            steps {
               echo "testingthe code"
              
            }
        }
        
 

        
         stage('deploying the code') {
            steps {
               echo "deploying the code"
               sh "docker compose down"
               sh "docker compose up -d"
              
            }
        }
    }
}
