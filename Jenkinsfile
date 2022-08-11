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
                withCredentials(credentialsId: 'directed-fabric-357018', variables: {'PROJECT_ID': '${PROJECT_ID}'}) {
                    sh "docker login -u eugeniubraga --password-stdin"{
                    sh "docker push eugeniubraga/ui"}
                }
            }
        }
    }
