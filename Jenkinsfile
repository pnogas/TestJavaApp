pipeline {
    agent {
        node {
            label 'master'
        }
    }
    environment {
        env.PATH = env.PATH + ";c:\\Windows\\System32"
    }

    options {
        buildDiscarder logRotator(
                    daysToKeepStr: '7',
                    numToKeepStr: '10'
            )
    }

    stages {
        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/master']],
                    userRemoteConfigs: [[url: 'https://github.com/pnogas/TestJavaApp.git']]
                ])
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    bat 'gradlew sonarqube'
                }
            }
        }
    }
}