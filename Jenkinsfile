pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/amanpatelitofficial/Portfoli-aman.git", branch: "jenkins"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t aman"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker tag flaskapp ${env.dockerHubUser}/flaskapp:latest"
                    sh "docker push ${env.dockerHubUser}/flaskapp:latest" 
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
