pipeline{
    agent any
    
    stages{
        stage("Clone code"){
          steps{
              echo "clonning the code"
              git url:"https://github.com/letswander012/django-notes-app.git", branch:"main"
          }  
        }
        stage("build"){
            steps{
                echo "Building the code"
                sh "docker build -t my-notes-app ."
            }
            
        }
        stage("Push"){
            steps{
                echo "pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"Dockerhub",passwordVariable:"DockerhubPass",usernameVariable:"DockerhubUser")])
               { sh "docker tag my-notes-app ${env.DockerhubUser}/my-notes-app:latest"
                   sh "docker login -u ${env.DockerhubUser} -p ${env.DockerhubPass}"
                   sh "docker push ${env.DockerhubUser}/my-notes-app:latest"
               }
            }
            
        }
        stage("deploy"){
            steps{
                echo "deploying the code"
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}
