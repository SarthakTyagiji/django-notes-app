pipeline{
    agent any
    
    stages{
        stage("Code"){
            steps{
                echo"Cloning the Code"
                git url:"https://github.com/LondheShubham153/django-notes-app.git",branch:"main"
                
            }
    } 
        stage("build"){
            steps{
                echo"Build the code"
                sh "docker build -t notes-app ."
                
            }
        
    }
       stage("Push to Docker Hub") {
    steps {
        echo "Pushing the code to Docker Hub"
        withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerhubPass', usernameVariable: 'dockerhubuser')]) {
            // Login to DockerHub
            sh "docker tag notes-app ${env.dockerhubuser}/notes-app:latest"
            sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubPass}"
            sh "docker push ${env.dockerhubuser}/notes-app:latest "
            // Additional steps for pushing the code to DockerHub can be added here
        
    }
}

        
    }
         stage("Deploy"){
             steps{
                 echo "Deploy the code"
                 sh "docker-compose down && docker-compose up -d"
                 
             }
        
    }
        
}
}
