pipeline {
    agent any
    environment {
        REPO_URL = 'https://github.com/Sravan40/app.git'
        MYSQL_DEPLOYMENT_FILE = 'app/project1/mysql-deployment.yaml'
        PYTHON_DEPLOYMENT_FILE = 'app/project1/python-deployment.yaml'
        SERVICE_FILE = 'app/project1/service.yaml'
    }
    stages {
        stage('Pull and Build') {
            steps {
                script {
                    echo 'Removing existing app directory...'
                    sh 'rm -rf app'
                    echo 'Cloning repository...'
                    sh "git clone ${REPO_URL}"
                    dir('app/project1') {
                        echo 'Building Docker image...'
                        sh 'docker build -t myappv1 .'
                    }
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    echo 'Logging in to Docker Hub...'
                    sh "docker login -u sravan40 -p Sravan@4070"
                    echo 'Pushing Docker image to Docker Hub...'
                    sh 'docker tag myappv1 sravan40/myappv1:latest'
                    sh 'docker push sravan40/myappv1:latest'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    echo "KUBECONFIG Environment Variable: ${env.KUBECONFIG}"
                    echo 'Creating namespaces...'
                    sh "kubectl create namespace sql"
                    sh "kubectl create namespace python"
                    
                    echo 'Deploying MySQL database...'
                    sh "kubectl apply -f ${MYSQL_DEPLOYMENT_FILE} -n sql"
                    
                    echo 'Deploying Python application...'
                    sh "kubectl apply -f ${PYTHON_DEPLOYMENT_FILE} -n python"
                    sh "kubectl apply -f ${SERVICE_FILE} -n python"
                }
            }
        }
    }
}
