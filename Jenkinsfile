pipeline {
    agent any
    environment {
        GITHUB_CREDENTIALS = credentials('sravan40')
        DOCKER_HUB_CREDENTIALS = credentials('sravan40')
    }
    stages {
        stage('Pull and Build') {
            steps {
                script {
                    echo 'Cloning repository...'
                    sh 'git clone https://github.com/Sravan40/app.git'
                    dir('app/project1') {
                        echo 'Building Docker image...'
                        sh 'sudo docker build -t myappv1 .'
                    }
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    echo 'Logging in to Docker Hub...'
                    sh "sudo docker login -u ${DOCKER_HUB_USERNAME} -p ${DOCKER_HUB_PASSWORD}"
                    echo 'Pushing Docker image to Docker Hub...'
                    sh 'sudo docker tag myappv1 ${DOCKER_HUB_USERNAME}/myappv1:latest'
                    sh 'sudo docker push ${DOCKER_HUB_USERNAME}/myappv1:latest'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying Docker image...'
                    // Add deployment steps here (e.g., docker run command)
                }
            }
        }
    }
}
