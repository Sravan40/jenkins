pipeline {
    agent any
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
                    sh "sudo docker login -u sravan40 -p Sravan@4070"
                    echo 'Pushing Docker image to Docker Hub...'
                    sh 'sudo docker tag myappv1 sravan40/myappv1:latest'
                    sh 'sudo docker push sravan40/myappv1:latest'
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
