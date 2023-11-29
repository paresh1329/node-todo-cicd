pipeline {
    agent any
    stages {
        stage("Code"){
           steps{
               git 'https://github.com/paresh1329/node-todo-cicd.git'
               echo 'code has been cloned'
               
           } 
        }
        stage("Build and Test"){
          steps{
              sh "docker build -t node-app ." 
              echo 'Image build and testing has been done'
              
          }  
          
        }
        stage("Scan Image"){
          steps{
              echo 'Image scanning has been done'
              
          }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub" ,passwordVariable:"dockerHubPass" ,usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag node-app:latest ${env.dockerHubUser}/node-app:latest"
                sh "docker push ${env.dockerHubUser}/node-app:latest"
                echo 'Image pushed to DockerHub'
                }
                
            }
        }
        stage("Deploy"){
           steps{
               sh "docker-compose down && docker-compose up -d "
               echo 'Application has been deployed'
               
           } 
        }
    }
                
}
