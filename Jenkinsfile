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
                // # The next line updates PATH for the Google Cloud SDK.
                sh "source '[path-to-my-home]/google-cloud-sdk/path.bash.inc'"
                // # The next line enables bash completion for gcloud.
                sh "source '[path-to-my-home]/google-cloud-sdk/completion.bash.inc'"
                sh "gcloud auth activate-service-account directed-fabric-357018 --key-file=GC_KEY"
                sh "docker tag eugeniubraga/ui gcr.io/directed-fabric-357018/ui:latest"
                sh "docker push gcr.io/directed-fabric-357018/apps"
                }
            }
        }
    }