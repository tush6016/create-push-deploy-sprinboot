pipeline {
    tools {
        maven 'Maven3'
    }
    agent any
    environment {
        registry = "318336405776.dkr.ecr.ap-south-1.amazonaws.com/production-repos"    
    }

    stages {
        stage('clone git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/tush6016/springboot-app.git']]])
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('build Image') {
            steps {
                script {
                    dockerImage = docker.build registry
                }
            }
        }
        stage('Push to ECR') {
            steps {
                script {
                    sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 318336405776.dkr.ecr.ap-south-1.amazonaws.com'
                    sh 'docker push 318336405776.dkr.ecr.ap-south-1.amazonaws.com/production-repos:latest'
                }
            }
        }
    }
}
