pipeline {
    agent any
    
    environment {
        registry = "318336405776.dkr.ecr.us-west-2.amazonaws.com/aaaa"    
    }

    stages {
        stage('clone git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/tush6016/springboot-app.git']]])
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
                    sh 'aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 318336405776.dkr.ecr.us-west-2.amazonaws.com'
                    sh 'docker push 318336405776.dkr.ecr.us-west-2.amazonaws.com/aaaa:latest'
                }
            }
        }
    }
}
