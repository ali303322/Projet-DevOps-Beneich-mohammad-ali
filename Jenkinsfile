pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Clonage du projet depuis GitHub'
                git branch: 'dev', url: 'https://github.com/user/ton-projet.git'
            }
        }

        stage('Build & Test') {
            steps {
                echo 'Build avec Maven'
                sh 'mvn clean install'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }
}
