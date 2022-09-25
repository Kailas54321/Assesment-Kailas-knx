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
             sh 'docker build -t test1:$BUILD_NUMBER .'
            }
          }
           /*  stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}*/
            stage('push') { 
            steps {
              sh 'docker tag test1:$BUILD_NUMBER kailas54321/test1:$BUILD_NUMBER'
              //sh'echo $dockerhub_PSW | sudo docker login -u $dockerhub_PSW -p ${dockerhub}'
              //sh'echo $dockerhub_PSW sudo docker login -u $dockeecho $dockerhub_PSW rhub_USR -p ${dockerhub}'
              // This step should not normally be used in your script. Consult the inline help for details.
              sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'  
              //witsh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'hDockerRegistry(credentialsId: 'dockerhub-jenkin', url: 'https://hub.docker.com/repository/docker/kailas54321/test1') {
    // some block
}
              sh'docker push kailas54321/test1:$BUILD_NUMBER'

            }
          }
          stage('pull & deploy') { 
            steps {
             
              sh'docker pull kailas54321/test1:$BUILD_NUMBER'
              sh'docker run -d -p 80:80 kailas54321/test1:$BUILD_NUMBER'

            }
          }
      
      } 
    