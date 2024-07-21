pipeline{
    agent any
    
    stages{
        stage("Code"){
            steps {
                echo "clone the code"
                git url: "https://github.com/62062331/django-notes-app.git", branch: "dev"
            }
        }
        stage("Build"){
            steps {
                echo "buiilding the code"
                sh "docker build -t mynotes-app ."
            }
        }
        stage("Pushing the code to dockerhub"){
            steps {
                echo "pushing the code to dockerhub"
                withCredentials([usernamePassword(credentialsId: 'DockerHub-ID', usernameVariable: 'DockerHubUser', passwordVariable: 'DockerHubPass')]) {
                sh "docker tag mynotes-app ${DockerHubUser}/mynotes-app:latest"     
                sh "docker login -u ${DockerHubUser} -p ${DockerHubPass}"
                sh "docker push ${DockerHubUser}/mynotes-app:latest"
                }
            }
        }
        stage("deploy"){
            steps {
                  echo "deployment of the code"
                  echo "Final development of container"
//                  sh "docker run -d -p 8000:8000 docker8145/mynotes-app:latest"
                  sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
