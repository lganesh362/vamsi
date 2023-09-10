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
        stage('NPM:Config') {
            steps{
                script {
                    withCredentials([usernamePassword(credentialsId: 'nexustoken01', passwordVariable: 'Pycube123$', usernameVariable: 'vamsi_vemula')]) {   
                        sh '''
                            set +x
                            # Make an API call to Nexus to get the authentication token
                            token=\$(curl -s -k -X POST -u \$nexustoken01:\$Pycube123$ http://100.26.159.217:8081/service/rest/v1/security/token)
                            echo "//http://100.26.159.217:8081/repository/sonarQube-nodeJS/:_authToken=\$token" >> .npmrc
                        '''
                    }
                }
            }
        }
        // stage('UploadArtifcatsintoNexus'){
        //     steps{
        //         sh "npm publish"
        //     }
        // } 
        // stage('Authenticate with npm registry') {
        //     steps {
        //         script {
        //             // Use the npm adduser command to authenticate
        //             sh 'npm adduser'
        //             sh ''
        //         }
        //     }
        // }
        stage('Configure npm credentials') {
            steps {
                script {
                    // Set the registry URL and credentials
                    sh 'npm config set registry http://100.26.159.217:8081/repository/sonarQube-nodeJS/'
                    sh 'npm login --registry http://100.26.159.217:8081/repository/sonarQube-nodeJS/ --scope=vamsi.drg1997@gmail.com --always-auth -u vami_vemula -p Pycube123$'
                }
            }
        }
        stage('Install and build') {
            steps {
                script {
                    // Run npm install and other npm commands as needed
                    sh 'npm install'
                    sh 'npm build'
                    // Add more npm commands here if necessary
                }
            }
        }
    }
}

