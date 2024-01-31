pipeline {
    agent any
    
    environment {
        SERVICE_ACCOUNT_GCP = credentials('GCP_SERVICE_ACCOUNT')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'docker build -t gcr.io/main-presence-408704/hotel-website:${BUILD_NUMBER} .'
            }
        }
        stage('Push') {
            steps {
                echo 'Push..'
                sh 'cat "$SERVICE_ACCOUNT_GCP" | docker login -u _json_key --password-stdin https://gcr.io'  
                sh 'docker push gcr.io/main-presence-408704/hotel-website:${BUILD_NUMBER}'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'docker docker run -d -p 80:80 hotel-website:${BUILD_NUMBER}'
                // sh "sed -i 's/tagnumber/${BUILD_NUMBER}/g' .devops/deployment.yaml"
                // sh 'kubectl apply -f .devops/deployment.yaml'
                // sh 'kubectl apply -f .devops/service.yaml'
            }
        }
    }
}
