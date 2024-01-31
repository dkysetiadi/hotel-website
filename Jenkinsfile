pipeline {
    agent any

    environment {
        GCP_SERVICE_ACCOUNT = credentials('SERVICE_ACCOUNT_GCP')
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'docker build -t gcr.io/ferrous-module-395010/hotel-website:${BUILD_NUMBER} .'
            }
        }
        stage('Push') {
            steps {
                echo 'Testing..'
                sh 'cat "$GCP_SERVICE_ACCOUNT" | docker login -u _json_key --password-stdin https://gcr.io'  
                sh 'docker push gcr.io/ferrous-module-395010/hotel-website:${BUILD_NUMBER}'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh "sed -i 's/tagnumber/${BUILD_NUMBER}/g' .devops/deployment.yaml"
                sh 'kubectl apply -f .devops/deployment.yaml'
                sh 'kubectl apply -f .devops/service.yaml'
            }
        }
    }
}
