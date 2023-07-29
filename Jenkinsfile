pipeline {
    agent any

    stages {
        stage('CODE') {
            steps {
                echo 'CLONING THE CODE'
                git url:"https://github.com/AKSHAY648outlook/django-notes-app.git" , branch: "main"
            }
        }
        stage('BUILD') {
            steps {
                echo 'BUILD THE CODE'
                sh "docker build -t my-notes-app ."
            }
        }
        stage('PUSH THE CODE') {
            steps {
                echo 'PUSH THE CODE TO DOCKER HUB'
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-notes-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push  ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
        stage('DEPLOY') {
            steps {
                echo 'DEPLOY ThE CODE'
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
