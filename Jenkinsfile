@Library('shared-library') _

node('ws') {

env.COMPONENT="cart"   // this is how variable is declared and this we can call from shared library
env.APPTYPE="nodejs"
env.TAG_NAME="latest"
// env.AWS_ACCESS_KEY_ID = credentials('Access_key')
// env.AWS_SECRET_ACCESS_KEY = credentials('Secret_access_key')
// call is the function that will be called by default. so, we are declaring the entire pipeline in the vars/nodejs.groovy
// env.NEXUS_URL = "172.31.38.109"
// env.SONAR_URL = "172.31.38.100"
// nodejs()
// withCredentials{(credentialsId: 'AWC_CREDS')}
stage('Login to ECR') {
        //withCredentials([usernameId: 'AWS_CREDS', passwordVariable: 'AWS_ACCESS_KEY_ID', fileCredentialId: 'AWS_CREDS', secretFileVariable: 'AWS_SECRET_ACCESS_KEY']) {
        sh "echo Authenticating To ECR"
        sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 851725330688.dkr.ecr.us-east-1.amazonaws.com"
     
      //  }
docker()

      }
}