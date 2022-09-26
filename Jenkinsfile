pipeline {
    
        agent any
        
        
        environment{
        	dockerhub=credentials('dockerhub')
           }
        stages {
          stage('pull-code') { 
            steps {
                git branch: 'main', credentialsId: 'Github_tkn', url: 'https://github.com/Kailas54321/Assesment-Kailas-knx.git'
          }
         
        }
        stage('Build') { 
            steps {
             sh 'docker build -t knx1:$BUILD_NUMBER .'
            }
          }
          
           stage('push') { 
            steps {
              sh 'docker tag knx1:$BUILD_NUMBER kailas54321/knx1:$BUILD_NUMBER'
              //sh'echo $dockerhub_PSW | docker login -u $dockerhub_PSW -p ${dockerhub}'
              sh 'chmod 666 /var/run/docker.sock'
              sh 'cat password.txt | docker login --username kailas54321 -p --password-stdin'
              //sh'echo $dockerhub_PSW docker login -u $dockeecho $dockerhub_PSW rhub_USR -p ${dockerhub}'
              sh'docker push kailas54321/knx1:$BUILD_NUMBER'

            }
          }
          stage('pull & deploy') { 
            steps {
             
              sh'docker pull kailas54321/knx1:$BUILD_NUMBER'
              sh'docker run -d -p 80:80 kailas54321/knx1:$BUILD_NUMBER'

            }
          }
          
      } 
    }