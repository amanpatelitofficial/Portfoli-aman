pipeline {
    agent any
    
   
    
    
    stages {
        stage('clean workspace') {
            steps {
                cleanWs()
            }
        }
        
        stage('Checkout from Git') {
            steps {
                git branch: 'main', url: 'https://github.com/amanpatelitofficial/Portfoli-aman.git'
            }
        }
        
        stage("Docker Build & Push"){
            steps{
                script{
                     withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){   
                       sh "docker build -t demo-app ."
                       sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                       sh "docker tag demo-app amanpatelitprofessional/demo-app:latest "
                       sh "docker push amanpatelitprofessional/demo-app:latest "
                    }
                }
            }
            
        }
        
        stage('Deploy to container'){
            steps{
                sh 'docker run -d --name demo-app -p 8081:80 amanpatelitprofessional/demo-app:latest'
            }
        }
}
}
