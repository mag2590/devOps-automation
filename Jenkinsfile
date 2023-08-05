pipeline {
    agent any
    tools{
        maven 'apache-maven-3.9.2'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mag2590/devOps-automation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t mag443/devops-integration .'
                }
            }
        }
        stage('Push image to Docker Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u mag443 -p ${dockerhubpwd}'

}
                   sh 'docker push mag443/devops-integration'
                }
            }
        }

    }
}
