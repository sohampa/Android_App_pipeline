// comment added
pipeline {

    environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
        }
    agent {
        label 'Soham-Node'
    }
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

//        stage('compile'){
//            steps{
//                echo "COMPILE"
//                sh "mvn clean compile"
            // }


//        stage('test'){
//            steps{
//                echo "Test"
//                sh "mvn clean test"
        //     }
        // }
//         stage('Sonar Analysis') {
//             steps {
//                 sh 'mvn clean install'
//                 sh 'mvn sonar:sonar -Dsonar.token=da31b7ebbcb8cb3701d8ef9ae23426fdceed40c1'
//             }
//         }

//        stage('package'){
//            steps{
//                echo 'Pakage'
//                sh 'mvn clean package'   
        //     }
        // }
}
