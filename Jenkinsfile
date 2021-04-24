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
                    withCredentials([usernamePassword( credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                     docker.withRegistry( '', 'dockerhub' )
                     sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                     dockerImage.push()
                    }
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
