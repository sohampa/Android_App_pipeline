// comment added
pipeline {
    environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
        }
    agent any
    tools {
        gradlew "gradle"
        jdk "jdk-17"
    }
    stages {
        stage('SonarQube Analysis'){
            steps{
                echo "SonarQube"
                gradlew sonarqube
            }
        }
}
}
