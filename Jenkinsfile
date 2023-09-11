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
                script {
                    // Check the quality gate status
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error "Quality Gate failed: ${qg.status}"
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
}
