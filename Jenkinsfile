pipeline {
    agent any
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/chumaedeogu/node-todo-cicd.git", branch: "master"
                echo 'bhaiyya code clone ho gaya'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t new-test ."
                echo 'code build by chuma'
            }
        }
        stage("scan image"){
            steps{
                echo 'image scanning ho gayi'
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag chumaedeogu/new-test chumaedeogu/new-test"
                sh "docker push chumaedeogu/new-test"
                echo 'image push ho gaya'
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'deployment ho gayi'
            }
        }
    }
}
