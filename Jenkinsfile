pipeline {
    agent any
    stages {
        stage("Code"){
           steps{
               git 'https://github.com/paresh1329/node-todo-cicd.git'
               echo 'bhaiya code clone ho gaya'
               
           } 
        }
        stage("Build and Test"){
          steps{
              sh "docker build -t node-app ." 
              echo 'code build bhi ho gaya'
              
          }  
          
        }
        stage("Scan Image"){
          steps{
              echo 'Image scanning ho gayi'
              
          }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub" ,passwordVariable:"dockerHubPass" ,usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag node-app:latest ${env.dockerHubUser}/node-app:latest"
                sh "docker push ${env.dockerHubUser}/node-app:latest"
                echo 'code push ho gaya'
                }
                
            }
        }
        stage("Deploy"){
           steps{
               sh "docker-compose down && docker-compose up -d "
               echo 'deployment ho gayi'
               
           } 
        }
    }
                
}
