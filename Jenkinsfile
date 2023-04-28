pipeline {
    agent any
    tools{
        maven 'maven'
    }
    
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/syedfarogh/MyspringRepo.git']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t faroghzaidi786/devops-integration .'
                }
            }
        }
       stage('Push image to hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u faroghzaidi786 -p ${dockerhubpwd}'
                        
                    }
                    sh 'docker push faroghzaidi786/kubernetes'
                }
            }
        }
