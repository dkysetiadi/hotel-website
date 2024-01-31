pipeline {
    agent any
    
    environment {
        SERVICE_ACCOUNT_GCP = credentials('SERVICE_ACCOUNT_GCP')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'docker build -t gcr.io/main-presence-408704/mediplus:${BUILD_NUMBER} .'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'cat "$SERVICE_ACCOUNT_GCP" | docker login -u _json_key --password-stdin https://gcr.io'  
                sh 'docker push gcr.io/main-presence-408704/mediplus:${BUILD_NUMBER}'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
