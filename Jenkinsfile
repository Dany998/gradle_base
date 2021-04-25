pipeline {
    
  environment {
    
    registry = "931524/docker_practice"
    registryCredential = 'dockerhub'
    dockerImage = '' 
   
  }
    agent any
  
    stages {
        
        stage('Clone') {
            
              steps {
               
                   checkout scm
              }
        }
        
        stage('Build') {
            
            steps {
                
                script {
                      dockerImage = docker.build registry + ":$BUILD_NUMBER"
                 }
            }
        }
        
        stage('Deploy') {
            
            steps {
                
                script {
                     docker.withRegistry( '', registryCredential )
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
