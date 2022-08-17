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
                    withCredentials([string(credentialsId: 'docker_hub', variable: 'dockerhub')]) {
                    sh "docker login -u eugeniubraga -p ${dockerhub}"
                        }
                    sh "docker push eugeniubraga/ui:latest"
                    }
                }
                }
        stage('Deploy to GKE') {
            steps {
                sh "sed -i s/tagversion/${env.BUILD_ID}/g manifest.yaml"
                step([
                    $class: "KubernetesEngineBuilder",
                            prjectId: env.PROJECT_ID,
                                clusterName: env.CLUSTER_NAME,
                                location: env.LOCATION,
                                credentialsId: env.CREDENTIALS_ID,
                                manifestPattern: "manifest.yaml",
                                verfyDeployment: true
                                ])
            }
            }
        }
}