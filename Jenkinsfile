pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_TAG', description: 'ENTER THE IMAGE TAG!')
    }
    

    stages {

        stage('CLEANUP WORKSPACE'){
            steps{
                script{
                    cleanWs()
                }
            }
        }

        stage("CHECKOUT GIT REPO"){
            steps{
                git branch: 'main', url: "https://github.com/aakkiiff/main-application-config-files.git"
            }
        }

        stage('update image tag') {
            steps {
                sh 'cat ./k8s/deployment.yaml'
                sh "sed -i 's/jenkinstest.*/jenkinstest:${IMAGE_TAG}/g' ./k8s/deployment.yaml"
                sh 'cat ./k8s/deployment.yaml'

            }
        }

        stage('push to github') {
            steps {
                sh 'git config --global user.email jackakif@gmail.com'
                sh 'git config --global user.name aakkiiff'

                sh 'git checkout main'
                sh 'git add ./k8s/deployment.yaml'
                sh "git commit -m'updated image tag to ${IMAGE_TAG}'" 

                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'passwd', usernameVariable: 'username')]) {
            
                sh 'git push https://$username:$passwd@github.com/aakkiiff/main-application-config-files.git main'
                }
            }
        }
    }
}