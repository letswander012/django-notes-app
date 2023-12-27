pipeline{
    agent any
    stages{
    stage(" Clone Code"){
        steps{
            echo "clonning the code"
            git url:"https://github.com/letswander012/django-notes-app.git", branch: "main"
        }
    }
    stage("Build"){
        steps{
            echo "Building the code"
            sh "docker build -t my-note-app1 ."
        }
        
    }
    stage("push to docker hub"){
        steps{
            echo "Pushing the image to docker hub"
            withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
            sh "docker tag my-note-app1 ${env.dockerHubUser}/my-note-app1:latest"    
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
            sh "docker push ${env.dockerHubUser}/my-note-app1:latest"
        }
        }
        
    }
    stage("deploy"){
        steps{
            echo "deploying the container"
            sh "docker-compose down && docker-compose up -d"
        }
        
    }
    }
}
