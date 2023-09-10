pipeline {
    agent any
    tools {
        nodejs "NodeJs 20.6.1"
    }
    stages {
        stage ('remove npm package'){
            steps{
                sh "rm -rf package-lock.json"
                sh "npm cache clean --force"
                sh "npm uninstall -g global-package"
            }
        }
        stage('Build') {
            steps {
                // Your build steps here
                sh 'npm install -g'
            }
        }
        stage('sonar'){
            steps{
                sh 'npm run sonar'
            }
        }
        stage('Configure npm credentials') {
            steps {
                script {
                    // Set the registry URL
                    sh 'npm config set registry http://100.26.159.217:8081/repository/sonarQube-nodeJS/'

                    // Use the npm token credential
                    withCredentials([string(credentialsId: 'nexustoken-npmrc', variable: 'npmtoken')]) {
                    sh 'echo "//registry.npmjs.org/:_authToken=$npmtoken" > ~/.npmrc'
                    }
                }
            }
        }

        stage('Install and build') {
            steps {
                // Your npm-related build and install steps here
                // You can use npm commands without specifying credentials
                sh 'npm install'
            }
        }
    }
}

       