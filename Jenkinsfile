pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/varadvrd/node-todo-cicd.git", branch: "master"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t node-app-test-new"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"Varad@5005",usernameVariable:"varad5005")]){
                    sh "docker login -u ${env.varad5005} -p ${env.Varad@5005}"
                    sh "docker tag node-app-test-new ${env.varad5005}/node-app-test-new:latest"
                    sh "docker push ${env.varad5005}/node-app-test-new:latest" 
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
