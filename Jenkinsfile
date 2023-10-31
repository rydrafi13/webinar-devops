pipeline {
    agent any
    
    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/rydrafi13/webinar-devops.git'
            }
        }
        stage('Containerized Apps') {
            steps {
                sh '''
                docker compose build
                '''
            }
        }
        stage('Push Image') {
            steps {
                sh '''
                docker compose push
                '''
            }
        }        
        stage('Deploy Apps') {
            steps {
                sh '''
                docker compose up -d
                '''
            }
        }
        stage('Alert') {
            steps {
                discordSend description: 'Notified From Jenkins', footer: '', image: '', link: 'http://10.10.10.89:8080/job/build-apps/', result: 'SUCCESS|UNSTABLE|FAILURE|ABORTED', scmWebUrl: '', thumbnail: '', title: 'build-apps', webhookURL: 'https://discordapp.com/api/webhooks/1168761107662516345/t7xdaN68lrM-Fw21DoLaFhFTQ66hAeUV-DbiNasfY4AlfIo5A8AA6jglmWvAb4X9YLeo'
            }
        }        
    }
}