pipeline {
    tools {
        maven 'Maven3'
    }
    agent any
    environment {
          132271831471.dkr.ecr.us-east-2.amazonaws.com/dev-engg-tushar    
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
                    sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 132271831471.dkr.ecr.us-east-2.amazonaws.com'
                    sh 'docker push 132271831471.dkr.ecr.us-east-2.amazonaws.com/dev-engg-tushar:latest'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh 'mkdir tushar'
                    sh mkdir 'prec'
                    }
                }
            }
        }
    }
}
