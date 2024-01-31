pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'docker build -t gcr.io/ferrous-module-395010/hotel-website:${BUILD_NUMBER} .'   
            }
        }
        stage('Push') {
            steps {
                echo 'Push..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
