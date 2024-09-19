pipeline {
    
        agent {
            label 'ecs-agent'
        } 
        
        
        // environment{
        // 	dockerhub=credentials('dockerhub')
        //    }
        stages {
          stage('pull-code') { 
            steps {
                git branch: 'main', credentialsId: 'git-koken', url: 'https://github.com/Kailas54321/Assesment-Kailas-knx.git'
          }

        }
        stage('Build') { 
            steps {
             sh 'docker build -t knx:latest .'
            }
          }
          
        //    stage('push') { 
        //     steps {
        //       sh 'export AWS_ACCESS_KEY_ID=$AWS_ECR_CRED'
        //       sh 'export AWS_SECRET_ACCESS_KEY=$AWS_ECR_CRED'
        //       sh 'ECR_LOGIN_CMD=$(aws ecr get-login-password --region us-east-2)'
        //       sh 'echo "$ECR_LOGIN_CMD" | docker login --username AWS --password-stdin 079200857347.dkr.ecr.us-east-2.amazonaws.com'
        //       sh 'docker tag knx:latest 079200857347.dkr.ecr.us-east-2.amazonaws.com/knx:latest'

        //     }
        //   }
        stage('push') { 
            steps {
             // sh 'docker tag knx:$BUILD_NUMBER kailas54321/knx:$BUILD_NUMBER'
              //sh'echo $dockerhub_PSW | docker login -u $dockerhub_PSW -p ${dockerhub}'
             // sh 'sudo chmod 666 /var/run/docker.sock'
             // sh 'cat password.txt | docker login --username kailas54321 --password-stdin'
              //sh'echo $dockerhub_PSW docker login -u $dockeecho $dockerhub_PSW rhub_USR -p ${dockerhub}'
             // sh'docker push kailas54321/knx-task:$BUILD_NUMBER'
                // sh 'aws ecr get-login --region us-east-2 --profile Kailas | docker login --username AWS --password-stdin 079200857347.dkr.ecr.us-east-2.amazonaws.com'
              //  sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 079200857347.dkr.ecr.us-east-2.amazonaws.com'
                sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 079200857347.dkr.ecr.us-east-2.amazonaws.com'
                sh 'docker tag knx:latest 079200857347.dkr.ecr.us-east-2.amazonaws.com/knx:latest'
                sh 'docker push 079200857347.dkr.ecr.us-east-2.amazonaws.com/knx:latest'
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
                    
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'AWS_ECR_CRED']]){
                        
                        def cluster = 'ECS_CLUSTER' 
                        def serviceName = 'task-service' 
                        def taskDefinition = 'ecs-task' 
                        def region = 'us-east-2' 

                        
                        sh "aws --region ${region} ecs update-service --cluster ${cluster} --service ${serviceName} --task-definition ${taskDefinition}"
                    }
                }
            }
        }   
    }
}
