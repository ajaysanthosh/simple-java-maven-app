pipeline {
    agent any
    tools {
        maven 'Maven 3.8'
    }
    stages {
        stage('Code Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'd8d4ca02-842b-41e9-a898-31233eab8e35', url: 'https://github.com/ajaysanthosh/simple-java-maven-app.git']]])
            }
        }
        stage('Build Code') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('print') {
            steps {
                sh 'echo Completed Successfully'
            }
        }
        stage('Email') {
            steps {
                emailext body: 'Build is done', subject: 'Build Completed Sucessfully for Pipeline', to: 'ajaysanthosh01@gmail.com'
            }
        }

    }
}
