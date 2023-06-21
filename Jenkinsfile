pipeline {
    
        agent any
        
        
        environment{
        	dockerhub=credentials('dockerhub')
           }
        stages {
          stage('pull-code') { 
            steps {
                git branch: 'main', credentialsId: 'abc_tkn', url: 'https://github.com/Kailas54321/Assesment-Kailas-knx.git'
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
              sh 'sudo chmod 666 /var/run/docker.sock'
             // sh 'cat password.txt | docker login --username kailas54321 --password-stdin'
              //sh'echo $dockerhub_PSW docker login -u $dockeecho $dockerhub_PSW rhub_USR -p ${dockerhub}'
              sh'docker push kailas54321/knx1:$BUILD_NUMBER'

            }
          }
    //       stage('pull & deploy') { 
    //         steps {
             
    //           sh'docker pull kailas54321/knx1:$BUILD_NUMBER'
    //           sh'docker run -itd -p 87:80 kailas54321/knx1:$BUILD_NUMBER'

    //         }
    //       }
          
    //   } 
    // }

stage('Deploy to ECS') {
            steps {
                script {
                    // Deploy the Docker image to ECS using the ECS plugin
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'AWS_ECR_CRED']]){
                        // Configure ECS deployment
                        def cluster = 'ecs_cluster' // Replace with your ECS cluster name
                        def serviceName = 'my-ecs-service' // Replace with your ECS service name
                        def taskDefinition = 'task-de' // Replace with your Task Definition ARN
                        def region = 'us-east-2' 

                        // Update ECS service with the new task definition
                        sh "aws --region ${region} ecs update-service --cluster ${cluster} --service ${serviceName} --task-definition ${taskDefinition}"
                    }
                }
            }
        }   
    }
}
