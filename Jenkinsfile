@Library("sharedjenkins") _
pipeline {
    
    agent { label "jenkins-agent-1"}
    
    stages {        
        stage("Code") {
            steps {
                script{
                    clone("https://github.com/saadaltafofficial/django-notes-app.git", "main")
                }
            }
        }
        stage("Build") {
            steps {
                withCredentials([usernamePassword('credentialsId': "dockerhub-cred",
                usernameVariable: "DOCKER_USER",
                passwordVariable: "IGNORE_PASS")]){
                script {
                    docker_build("notes-app", "latest", "${DOCKER_USER}")
                    }
                }
             
            }
        }        
        stage("Push to Docker Hub") {
            steps {
               script {
                   docker_push("notes-app", "latest", "ignismeow")
               }
            }
        }
         stage("Deploy") {
            steps {
                script {
                    docker_compose()
                }
            }
        }
    }
    
}
