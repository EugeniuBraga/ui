pipeline {
    agent any
    environment {
        PROJECT_ID = 'directed-fabric-357018'
        CLUSTER_NAME = 'telega-cluster'
        LOCATION = 'us-central1-c'
        CREDENTIALS_ID = 'directed-fabric-357018'
        PATH = '/sbin:/bin:/usr/sbin:/usr/bin:/opt/google-cloud-sdk/bin'
    }
    stages{
        stage('Build Docker Image') {
            steps {
                sh "docker build -t gcr.io/directed-fabric-357018/ui:latest ."
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([file(credentialsId: 'GCP_KEY', variable: 'GCP_KEY')]) {
                        sh "gcloud auth activate-service-account --key-file=$GCP_KEY"
                    }
                    sh "docker push gcr.io/directed-fabric-357018/ui:latest"
                }
            }
        }
        // stage('Deploy to GKE') {
        //     steps {
        //         sh "sed -i s/tagversion/${env.BUILD_ID}/g manifest.yaml"
        //         step([
        //             $class: "KubernetesEngineBuilder",
        //                     projectId: env.PROJECT_ID,
        //                         clusterName: env.CLUSTER_NAME,
        //                         location: env.LOCATION,
        //                         credentialsId: env.CREDENTIALS_ID,
        //                         manifestPattern: "manifest.yaml",
        //                         verifyDeployment: true
        //                         ])
        //     }
        // }
    }
}