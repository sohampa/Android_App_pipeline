// comment added
pipeline {
    environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
        }
    tools {
        gradle "gradle"
        jdk "jdk-17"
    }
    agent any
    stages {
        stage('SonarQube Analysis'){
            steps{
                echo "SonarQube"                
                withSonarQubeEnv('SonarQubeServer') {
                    bat "gradlew sonarqube"
              }
            }
        }
        // stage("Quality Gate") {
        //     steps {
        //     //     timeout(time: 1, unit: 'HOURS') {
        //     //     waitForQualityGate abortPipeline: true }
                
        //          script {
        //                 echo "Checking Quality Gates"
        //                 def qg = waitForQualityGate()
        //                 if (qg.status != 'OK') {
        //                     error "Pipeline aborted due to quality gate failure: ${qg.status}"
        //                     echo "Quality Gate status updated" 
        //                 }
        //         }
        //     }
        // }
         stage('Build'){
            steps{
                echo "Build"
                bat "gradlew clean build"
            }
        }
        stage('Upload_Artifact') {
            steps {
                script{
               def server = Artifactory.server 'artifactory'

                def uploadSpec = """{
                  "files": [
                    {
                      "pattern": "app/build/outputs/apk/release/*.apk",
                      "target": "Soham-APK/"
                    }
                 ]
                }"""
                server.upload(uploadSpec) 
            }
            }
        }
}
    post{
        success{
            slackSend( channel: "#poc", token: "K4xlRQw5CWXfITGrtMgPHeLX", color: "good", message: "${custom_success_msg()}")
        }
        failure{
            slackSend( channel: "#poc", token: "K4xlRQw5CWXfITGrtMgPHeLX", color: "danger", message: "${custom_fail_msg()}")
        }
    }
}
def custom_success_msg()
{
  def JENKINS_URL= "http://172.27.59.109:8080/"
  def JOB_NAME = env.JOB_NAME
  def BUILD_ID= env.BUILD_ID

  def JENKINS_LOG= " Success: Job [${env.JOB_NAME}] Logs path: ${JENKINS_URL}/job/${JOB_NAME}/${BUILD_ID}/consoleText"
  echo ${JENKINS_LOG}
  return JENKINS_LOG

}
def custom_fail_msg()
{
  def JENKINS_URL= "http://172.27.59.109:8080/"
  def JOB_NAME = env.JOB_NAME
  def BUILD_ID= env.BUILD_ID

  def JENKINS_LOG= " Failure: Job [${env.JOB_NAME}] Logs path: ${JENKINS_URL}/job/${JOB_NAME}/${BUILD_ID}/consoleText"
  return JENKINS_LOG

}
