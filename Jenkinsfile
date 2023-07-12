pipeline {
    agent any
    stages{
        stage("clone code"){
            steps {
                echo "cloning the code"
                git url: "https://github.com/yogesh-pal/django-notes-app.git", branch: "main"
            }
        }
        stage("build"){
            steps{
                echo "build the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("push to docker hub"){
            steps{
                echo "pushing the code"
                withCredentials([usernamePassword(credentialsId:"docker-hub-id",usernameVariable:"dockerHubUser",passwordVariable:"dockerHubPass")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubpass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                    
                }
            }
        }
        stage("deploy the code"){
            steps{
                echo "deploying the code"
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
    }
}
