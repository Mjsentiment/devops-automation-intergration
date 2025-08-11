pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build maven project'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Mjsentiment/devops-automation-intergration.git']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'sudo docker build -t mikedevop/devops-integration .'
                }
            }
        }
        stage('push image to docker hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u mikedevop -p ${dockerhubpwd}'
}
                    sh 'docker push mikedevop/devops-integration'
                }
            }
        }
    }
}
