pipeline {
    agent any
    tools{
        maven 'maven_3_5_0'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Java-Techie-jt/devops-automation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t javatechie/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: '2479349d-644e-4c4e-a489-7efbb8bd4112', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u ravinder143 -p ${dockerhubpwd}'

}
                   sh 'docker push ravinder143/devops-integration'
                }
            }
        }
        
    }
}
