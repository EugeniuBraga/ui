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
                // sh "gcloud auth activate-service-account directed-fabric-357018 --key-file=.secrets/directed-fabric-357018-b40dd9a5e9cc.json"
                sh "gcloud auth configure-docker -q"
                sh "docker tag eugeniubraga/ui gcr.io/directed-fabric-357018/ui:latest"
                sh "docker push gcr.io/directed-fabric-357018/apps"
                }
            }
        }
    }