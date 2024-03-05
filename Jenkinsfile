pipeline{
    agent any
    
    
     environment {
    
        imageName = 'amanpatelitprofessional/demo-app'
        dockerHubCredentials = 'dockerhub'
        DOCKER_IMAGE = 'amanpatelitprofessional/demo-app'
        GIT_CREDENTIALS = credentials('githubkey')
        MAX_IMAGES_TO_KEEP = 5
    }
    
      stages {
        stage('Checkout') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/master']],
                        userRemoteConfigs: [[url: 'https://github.com/amanpatelitofficial/Portfoli-aman.git']],
                        extensions: [[$class: 'CleanCheckout']],
                        credentialsId: 'GIT_CREDENTIALS'
                    ])
                }
            }
        }

    

        
        stage('Build & Test') {
            steps {
                script {
                    
                    def DOCKER_IMAGE = "${imageName}:${BUILD_NUMBER}"
                    sh "docker build . -t ${DOCKER_IMAGE}"
                
                }
            }
        }
        
        
        stage('Push to Docker Hub') {
            steps {
                script {
                   withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                        def DOCKER_IMAGE = "${imageName}:${BUILD_NUMBER}"
                        sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                        sh "docker push ${DOCKER_IMAGE}"
                    }
                }
            }
        }
        
       stage('Deploy to container'){
            steps{
                sh 'docker run -d --name demo-app -p 8080:80 amanpatelitprofessional/demo-app:latest'
            }
        } 
       
        
    }
}

    

   

