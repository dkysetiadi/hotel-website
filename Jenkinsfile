pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building..' 
                sh 'docker build -t gcr.io/main-presence-408704/mediplus:${BUILD_NUMBER} .'
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
