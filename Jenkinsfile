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
        stage('Login Docker') {
            steps {
                sh "docker login -u eugeniubraga --password-stdin"
            }
        }
        stage('Push Docker Image') {
            steps {
                    sh "echo $docker | docker login -u eugeniubraga --password-stdin"{
                    sh "docker push eugeniubraga/ui"}
                }
            }
        stage('Deploy to K8s') {
            steps{
                sh "sed -i 'eugeniubraga/ui:latest' manifest.yaml"
                step([$class: 'KubernetesEngineBuilder',
                projectId: env.PROJECT_ID,                  
                clusterName: env.CLUSTER_NAME,
                location: env.LOCATION,
                manifestPattern: 'manifest.yaml',
                credentialsId: env.CREDENTIALS_ID,
                verifyDeployments: true
            ])
            }
        }
    }
}
