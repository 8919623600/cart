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
node {
        // env.AWS_ACCESS_KEY_ID = 'AWS_ACCESS_KEY_ID_ROBOSHOP'
        // env.AWS_SECRET_ACCESS_KEY = 'AWS_SECRET_ACCESS_KEY_ROBOSHOP'
        // env.REGION = 'us-east-1'
        git branch: "main" , url: "https://github.com/8919623600/${COMPONENT}.git"
        common.lintchecks()
        common.testcases()
        if (env.TAG_NAME != null) {
            stage("generating and publishing artifact")
            // label 'ws'
            if (env.APPTYPE == "nodejs") {
                sh "echo generating node artifacts"
                // sh "npm install"
            }
            else if(env.APPTYPE == "python") {
                    sh "echo Generating Artifacts"
                    sh "zip -r ${COMPONENT}-${TAG_NAME}.zip *.py *.ini requirements.txt"        
                } 
            else if(env.APPTYPE == "java") {
                    sh "mvn clean package"
                    sh "mv target/${COMPONENT}-1.0.jar ${COMPONENT}.jar"
                    sh "zip -r ${COMPONENT}-${TAG_NAME}.zip  ${COMPONENT}.jar"      
                }
            else if(env.APPTYPE == "angularjs") {
                    sh "cd static/"
                    sh "zip -r ../${COMPONENT}-${TAG_NAME}.zip *"
                }
            else { sh "echo Selected Component Type Doesnt Exist" }                        
        }
    stage('Login to ECR')
    
     {
        sh "echo Downloading the pem key file for DB Connectivity"
        sh "wget https://truststore.pki.rds.amazonaws.com/global/global-bundle.pem"
        sh "echo Authenticating To ECR"
        sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 851725330688.dkr.ecr.us-east-1.amazonaws.com"
        sh "docker build -t 851725330688.dkr.ecr.us-east-1.amazonaws.com/${COMPONENT}:${TAG_NAME} ."
        sh "docker push 851725330688.dkr.ecr.us-east-1.amazonaws.com/${COMPONENT}:${TAG_NAME}"
      
      }

    }
// docker()

      
}