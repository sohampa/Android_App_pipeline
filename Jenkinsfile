// comment added
pipeline {
    environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
        }
    agent any
    tools {
        gradle "gradle"
        jdk "jdk-17"
    }
    stages {
        stage('validate'){
            steps{
                echo "VALIDATE"
            }
        }
}
}
