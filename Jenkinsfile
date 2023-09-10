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
        stage('NPM: Config') {
  withCredentials([usernamePassword(credentialsId: admin, passwordVariable: 'Pycube123$', usernameVariable: 'NEXUS_USERNAME')]) {
    def token = sh(returnStdout: true, script: "set +x && curl -s -k -H \"Accept: application/json\" -H \"Content-Type:application/json\" -X PUT --data '{\"name\": \"$NEXUS_USERNAME\", \"password\": \"$NEXUS_PASSWORD\"}'
	http://100.26.159.217:8081/#admin/repository/repositories:sonarQube-nodeJS.user:$NEXUS_USERNAME 2>&1 | grep -po
	 '(?<=\"token\":\")[^\"]*'")
    sh "set +x && echo \"//http://100.26.159.217:8081/#admin/repository/repositories:sonarQube-nodeJS/:_authToken=$token\" >> .npmrc"
  }
}
           stage('UploadArtifcatsintoNexus'){
            steps{
            sh "npm publish"
            }
        } 
    }
}

