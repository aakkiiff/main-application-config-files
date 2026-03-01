pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_TAG', description: 'ENTER THE IMAGE TAG!')
    }

    stages {
        stage('update image tag') {
            steps {
                sh 'cat ./k8s/deployment.yaml'
                sh "sed -i 's/jenkinstest.*/jenkinstest:${IMAGE_TAG}/g' ./k8s/deployment.yaml"
                sh 'cat ./k8s/deployment.yaml'

            }
        }
    }
}
