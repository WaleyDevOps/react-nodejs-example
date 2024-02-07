#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        maven 'maven-3.9.6'
    }
    
    environment {
        IMAGE_NAME = 'waledevops/demo-app:node-app-2.0'
    }

    stages {
        stage('Testing app') {
            steps {
                script {
                        echo 'building application jar....'
                        
                }
            }
        }
        stage('Build image') {
                steps{
                    script {
                        echo 'building docker image...'
                        
                    }
                }
        }
            
        stage('Deploy') {
                steps{
                    script {
                        echo 'deploying docker image to EC2'
                        def dockerCmd = "docker run -p 3080:3080 -d ${IMAGE_NAME}"
                        sshagent (['ec2-server-key']) {
                            sh "ssh -o StrictHostKeyChecking=no ec2-user@18.201.234.153 ${dockerCmd}"
                        } 
                    }
                }
        }
    }
}


