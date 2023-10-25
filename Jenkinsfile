pipeline {
    agent any 
    stages {
        stage('Build') {
            steps {
                echo 'Running ls command...'
                sh 'ls'
                
                echo 'Printing the date...'
                sh 'date'
                
                echo 'Creating a directory named \'jenkins\'...'
                sh 'mkdir jenkins'
                
                echo 'Changing directory to \'jenkins\'...'
                dir('jenkins') {
                    echo 'Current directory (pwd) inside \'jenkins\':'
                    sh 'pwd'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add your test steps here
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Add your deployment steps here
            }
        }
    }
}
