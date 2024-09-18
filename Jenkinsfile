pipeline{
    agent{ 
        node{
    label "dev"
    }
        }
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/pariharrohit223/Django_cicd_for_jenkins_new.git", branch: "main"
                echo "code clone ho chuka h (jenkin file running from git hub jenkins file pariharohit30"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t pariharrohit30/notes-app-jenkins"
                echo "docker ke through image build ho gai"
            }
        }
       stage("Push to Docker hub"){
           steps{
               echo "pahucha di docker hub per"
               withCredentials(
                   [usernamePassword(
                       credentialsId:"dockerCreds",
                       passwordVariable:"dockerHubPass",
                       usernameVariable:"dockerHubUser"
                       )]
                   )
                   {
                       sh "docker image tag notes-app-jenkins:latest ${env.dockerHubUser}/notes-app:latest"
                       sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                       sh "docker push ${env.dockerHubUser}/notes-app-jenkins:latest"
                   }
               
           }
       }
        stage("Deploy"){
            steps{
                sh "docker compose up"
                echo "Docker compose commad chala di or app run ho gaya"
            }
        }
    }
    
}
