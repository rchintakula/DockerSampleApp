pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t nginxtest:latest .' 
                sh 'docker tag nginxtest rchintakula/nginxtest:latest'
                sh 'docker tag nginxtest rchintakula/nginxtest:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "rchintakula", url: "" ]) {
          sh  'docker push rchintakula/nginxtest:latest'
          sh  'docker push rchintakula/nginxtest:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 4030:80 rchintakula/nginxtest"
 
            }
        }
    }
}