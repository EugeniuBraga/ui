pipeline {
    agent any
    environment {
        PROJECT_ID = 'directed-fabric-357018'
        CLUSTER_NAME = 'telega-cluster'
        LOCATION = 'us-central1-c'
        CREDENTIALS_ID = 'directed-fabric-357018'
    }
    stages{
        stage('Build Docker Image') {
            steps {
                sh "docker build -t eugeniubraga/ui:latest ."
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([file(credentialsId: 'GC_KEY', variable: 'GC_KEY')]){
                sh "cat '$GC_KEY' | docker login -u _json_key --password-stdin https://gcr.io"
                sh "gcloud auth activate-service-account --key-file='$GC_KEY'"
                sh "gcloud auth configure-docker"
                echo "Pushing Docker Image"
                sh 'gcloud auth print-access-token'
                
                echo "Pushing image To GCR"
                // sh "sudo -s gcloud auth configure-docker"
                // sh "docker tag eugeniubraga/ui gcr.io/directed-fabric-357018/ui:latest"
                sh "docker push gcr.io/directed-fabric-357018/apps"
                }
            }
        }
    }
}