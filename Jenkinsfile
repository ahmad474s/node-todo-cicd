pipeline {
    agent { label 'agent-dev' 
    }
    stages {
        stage("Code") {
            steps{
            git url: 'https://github.com/ahmad474s/node-todo-cicd.git', branch: 'master'
            }
        }
        stage("Build & Test") {
            steps{
                sh 'docker build . -t ahmadsaeedch/node-todo-app-cicd:latest'
            }
        }
        stage("docker Login & Push image") {
            steps{
                 echo "login into docker hub and push image into docker Hub"
                 withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                 sh "docker login -u ${env.USERNAME} -p ${env.PASSWORD}"  
                 sh "docker push ahmadsaeedch/node-todo-app-cicd:latest"
                }             
            }
        }
        stage("Deploy") {
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }   
}
