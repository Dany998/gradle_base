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
               // <!-------- Cloning the repository ------------>
                   checkout scm
              }
        }
        
        stage('Build') {
            
            steps {
                // <!-------- Building the image ------------>
                script {
                      dockerImage = docker.build registry + ":$BUILD_NUMBER"
                 }
            }
        }
        
        stage('Deploy') {
            
            steps {
                // <!-------- Publishing the image to DockerHub ------------>
                script {
                      docker.withRegistry('', registryCredential) {
                      dockerImage.push()
                    }
                }         
            }
        }
        
        stage('Trash') {
            // <!-------- Removing the image from server ------------>
            steps{
                sh "docker rmi $dockerRegistry:$BUILD_NUMBER"
            }
        }
    }
}
