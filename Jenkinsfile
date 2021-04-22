pipeline {
    
  environment {
    
    dockerRegistry = 'https://hub.docker.com/repository/docker/931524/docker_practice'
    credentialsId = 'dockerhub'
    dockerImage = '' 
   
  }
    agent any
  
    stages {
        
        stage("Git repo") {
            
            steps {
                git 'https://github.com/Dany998/gradle_base.git'
                git 'update-index --chmod=+x gradlew'
            }
        }
        
        stage("Build") {
            
            steps {
            
                sh './gradlew build'
                
                script {
                      dockerImage = docker.build dockerRegistry + ":$BUILD_NUMBER"
                 }
            }
        }
        
        stage("Test") {
            
            steps {
                sh './gradlew clean test --no-daemon'
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
    }
}
