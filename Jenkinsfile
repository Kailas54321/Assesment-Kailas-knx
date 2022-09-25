pipeline {
    
        agent any
        
        
        environment{
        	dockerhub=credentials('dockerhub-jenkin')
           }
        stages {
          stage('pull-code') { 
            steps {
                git branch: 'main', credentialsId: 'Github_tkn', url: 'https://github.com/Kailas54321/Assesment-Kailas-knx.git'
          }
         
        }
        stage('Build') { 
            steps {
             sh 'sudo docker build -t test1:$BUILD_NUMBER .'
            }
          }
          
           stage('push') { 
            steps {
              sh 'sudo docker tag test1:$BUILD_NUMBER Kailas54321/test1:$BUILD_NUMBER'
              //sh'echo $dockerhub_PSW | sudo docker login -u $dockerhub_PSW -p ${dockerhub}'
              sh'echo $dockerhub_PSW sudo docker login -u $dockeecho $dockerhub_PSW rhub_USR -p ${dockerhub}'
              sh'sudo docker push Kailas54321/test1:$BUILD_NUMBER'

            }
          }
          stage('pull & deploy') { 
            steps {
             
              sh'sudo docker pull Kailas54321/test1:$BUILD_NUMBER'
              sh'sudo docker run -d -p 80:80 Kailas54321/test1:$BUILD_NUMBER'

            }
          }
          
      } 
    }