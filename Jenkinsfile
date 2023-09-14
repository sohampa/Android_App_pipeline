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
        stage("Quality Gate") {
            steps {
            //     timeout(time: 1, unit: 'HOURS') {
            //     waitForQualityGate abortPipeline: true }
                
                 script {
                        echo "Checking Quality Gates"
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                            echo "Quality Gate status updated" 
                        }
                }
            }
        }
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
            slackSend( channel: "#poc", token: "K4xlRQw5CWXfITGrtMgPHeLX", color: "good", message: " Successfully Build")
        }
    //     failure{
    //         slackSend( channel: "#poc", token: "K4xlRQw5CWXfITGrtMgPHeLX", color: "danger", message: "Alert Build Failure")
    //     }
    }
}
