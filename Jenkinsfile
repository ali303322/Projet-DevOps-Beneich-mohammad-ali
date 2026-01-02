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
        slackSend(
            channel: '#jenkins',
            message: "✅ Build & tests réussis pour ${env.JOB_NAME} (#${env.BUILD_NUMBER})"
        )
    }

    failure {
        slackSend(
            channel: '#jenkins',
            message: "❌ Échec du build ou des tests pour ${env.JOB_NAME} (#${env.BUILD_NUMBER})"
        )
    }
}

}
