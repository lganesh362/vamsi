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
    withCredentials([usernamePassword(credentialsId: 'nexustoken01', passwordVariable: 'Pycube123$', usernameVariable: 'admin')]) {   
    script {
    sh """
    set +x
    # Make an API call to Nexus to get the authentication token
    token=\$(curl -s -k -X POST -u \$nexustoken01:\$Pycube123$ http://100.26.159.217:8081/service/rest/v1/security/token)
    echo "//http://100.26.159.217:8081/repository/sonarQube-nodeJS/:_authToken=\$token" >> .npmrc
    """
  }
}
            }
        }
           stage('UploadArtifcatsintoNexus'){
            steps{
            sh "npm publish"
            }
        } 
    }
}

