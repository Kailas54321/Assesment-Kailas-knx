pipeline {
    
        agent any
        
        
        environment{
        	dockerhub=credentials('dockerhub')
           }
        stages {
          stage('pull-code') { 
            steps {
                git credentialsId: 'github_TKN', url: 'https://github.com/vishalsontakke26/Assessment-knx-devops-microservice-test.git'
          }
         
        }
        stage('Build') { 
            steps {
             sh 'sudo docker build -t test1:$BUILD_NUMBER .'
            }
          }
          
           stage('push') { 
            steps {
              sh 'sudo docker tag test1:$BUILD_NUMBER vishalsontakke/test1:$BUILD_NUMBER'
              //sh'echo $dockerhub_PSW | sudo docker login -u $dockerhub_PSW -p ${dockerhub}'
              sh'echo $dockerhub_PSW sudo docker login -u $dockeecho $dockerhub_PSW rhub_USR -p ${dockerhub}'
              sh'sudo docker push vishalsontakke/test1:$BUILD_NUMBER'

            }
          }
          stage('pull & deploy') { 
            steps {
             
              sh'sudo docker pull vishalsontakke/test1:$BUILD_NUMBER'
              sh'sudo docker run -d -p 80:80 vishalsontakke/test1:$BUILD_NUMBER'

            }
          }
          
      } 
    }