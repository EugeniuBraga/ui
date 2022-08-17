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
                script {
                    withCredentials([string(credentialsId: "dockerhub", variable: "dockerhub")]) {
                    sh "docker login -u eugeniubraga -p ${dockerhub}"
                        }
                    sh "docker push eugeniubraga/ui:latest"
                    }
                }
                }
            }
            // stage('Deploy to GKE') {
            //     steps {
            //         sh "gcloud container clusters get-credentials $CLUSTER_NAME --zone $LOCATION --project $PROJECT_ID"
            //         sh "kubectl apply -f deployment.yaml"
            //     }
            // }
        }