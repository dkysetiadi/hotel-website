pipeline {
    agent any
    
    environment {
        GCP_SERVICE_ACCOUNT = credentials('SERVICE_ACCOUNT_GCP')
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
                sh 'cat "$GCP_SERVICE_ACCOUNT" | docker login -u _json_key --password-stdin https://gcr.io'  
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
