pipeline {
    
  environment {
    
    dockerRegistry = 'https://hub.docker.com/repository/docker/931524/docker_practice'
    credentialsId = 'dockerhub'
    dockerImage = '' 
   
  }
    agent any
  
    stages {
        
        stage("Build") {
            
            steps {
                
                script {
                      dockerImage = docker.build dockerRegistry + ":$BUILD_NUMBER"
                 }
            }
        }
        
        stage("Deploy") {
            
            steps {
                
                script {
                     docker.withRegistry( '', credentialsId)
                     dockerImage.push()
                    
                }
            }
        }
        
        stage('Trash') {
            
            steps{
                sh "docker rmi $dockerRegistry:$BUILD_NUMBER"
            }
        }
    }
}
