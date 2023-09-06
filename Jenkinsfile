// comment added
pipeline {
    environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
        }
    tools {
        gradlew "gradle"
        jdk "jdk-17"
    }
    agent None
    stages {
        stage('SonarQube Analysis'){
            steps{
                echo "SonarQube"
                gradlew sonarqube
            }
        }
}
}
