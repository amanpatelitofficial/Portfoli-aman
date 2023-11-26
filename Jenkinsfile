pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/amanpatelitofficial/Portfoli-aman.git", branch: "main"
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
                    sh "docker tag aman ${env.dockerHubUser}/aman:latest"
                    sh "docker push ${env.dockerHubUser}/aman:latest" 
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "aman"
            }
        }
    }
}
