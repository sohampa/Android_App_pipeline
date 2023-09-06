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
                bat "gradlew sonarqube"
            }
        }
         stage('Build'){
            steps{
                echo "Build"
                bat "gradlew clean build"
            }
        }
}
}
