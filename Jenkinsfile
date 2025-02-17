pipeline {
    agent { label "vinod" }

    stages {
        stage("Code") {
            steps {
                echo "This is cloning the code"
                dir('devops') {  
                    git branch: 'main', url: 'https://github.com/Harshraj843112/django-notes-app.git'
                }
            }
        }
        stage("Build") {
            steps {
                echo "This is building the code"
                dir('devops') {  
                    sh "docker build -t notes-app:latest ."
                }
            }
        }
        stage("Push to DockerHub") {
            steps {
                echo "This is pushing the images to Docker Hub"
                withCredentials([usernamePassword(credentialsId: 'dockerHubCredentails', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    sh "docker image tag notes-app:latest $DOCKER_USER/notes-app:latest"
                    sh "docker push $DOCKER_USER/notes-app:latest"
                }
            }
        }
        stage("Deploy") {
            steps {
                echo "This is deploying the code"
            }
        }
    }
}
