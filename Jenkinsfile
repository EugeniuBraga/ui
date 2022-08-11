pipeline {
    agent any
    environment {
        PROJECT_ID = 'directed-fabric-357018'
        CLUSTER_NAME = 'telega-cluster'
        LOCATION = 'us-central1-c'
        CREDENTIALS_ID = 'directed-fabric-357018'
    }
    stage('Build image') {
        /* Build your image */

        app = docker.build("eugeniubraga/ui")
    }
    stage('Push image') {
    /* Push image using withRegistry. */
    docker.withRegistry('eugeniubraga', 'dockerhub') {
        app.push("${env.BUILD_NUMBER}")
        app.push("latest")
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
