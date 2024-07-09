@Library('shared-library') _

node('ws') {

env.COMPONENT="cart"   // this is how variable is declared and this we can call from shared library
env.APPTYPE="nodejs"
env.TAG_NAME="latest"
// call is the function that will be called by default. so, we are declaring the entire pipeline in the vars/nodejs.groovy
// env.NEXUS_URL = "172.31.38.109"
// env.SONAR_URL = "172.31.38.100"
// nodejs()
// withCredentials{(credentialsId: 'AWC_CREDS')}
stage('Login to ECR') {
    withCredentials([usernameId: 'aws-credentials', passwordVariable: 'AWS_ACCESS_KEY_ID', fileCredentialId: 'aws-credentials', secretFileVariable: 'AWS_SECRET_ACCESS_KEY']) {
      
    }
  }
docker()
}