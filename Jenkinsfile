#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    
    environment {
        IMAGE_NAME = 'waledevops/demo-app:node-app-2.0'
    }

    stages {
        stage('build app') {
           steps {
               script {
                    echo 'building application jar....'
                    buildJar()
                }
            }
        }
        stage('Build image') {
            
            }
            steps {
                script {
                    echo 'building docker image...'
                    buildImage(env.IMAGE_NAME)
                    dockerLogin()
                    dockerPush(env.IMAGE_NAME)
                }
            }
        }
        
        stage('Deploy') {
            steps {
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

