pipeline {
    agent any
    tools {
        nodejs "NodeJs 20.6.1"
    }
    stages {
        stage('Build') {
            steps {
                // Your build steps here
                sh 'npm install'
            }
        }
        stage('ExecuteSonarQubeReport'){
            withSonarQubeEnv(credentialsId: 'sonar') {
        sh "npm run sonar"}
        }
    }
}