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
    }
    post {
      always {
        discordSend description: 'Jenkins Pipeline Build', enableArtifactsList: true, footer: "Build ${JOB_NAME} #${BUILD_NUMBER}", image: '', link: env.BUILD_URL, result: currentBuild.currentResult, scmWebUrl: '', showChangeset: true, thumbnail: '', title: "${JOB_NAME} #${BUILD_NUMBER}", webhookURL: 'https://discord.com/api/webhooks/1167421282934079548/d2VMeAsU9Z1Qfm3aXvAKhOtisUh7_n3GRwB0hzXu33eUCFAsDobAaEQxMRgnXsbMREqT'
      }
    }        
}