pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'dev', url: 'https://github.com/user/ton-projet.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh 'cp target/ton-app.jar /opt/apps/'
            }
        }
    }

    post {
        success {
            slackSend channel: '#general', message: "✅ Build réussi pour ${env.JOB_NAME} !"
        }
        failure {
            slackSend channel: '#general', message: "❌ Échec du build pour ${env.JOB_NAME} !"
        }
    }
}
