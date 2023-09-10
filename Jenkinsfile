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
        stage('sonar'){
            steps{
                sh 'npm run sonar'
            }
        }
           stage('UploadArtifcatsintoNexus'){
            steps{
            sh "npm publish"
            }
        }
        stage('RunNodeJsApp'){
            steps{
                sh "npm run app.js &"
            }
        }
    }
}

