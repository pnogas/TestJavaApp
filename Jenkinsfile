pipeline {
    agent any
    stages {
        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: env.BRANCH_NAME]],
                    userRemoteConfigs: [[url: 'https://github.com/pnogas/TestJavaApp.git']]
                ])
            }
        }
        stage('Start Code Analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    bat 'gradlew.bat sonarqube'
                }
            }
        }
        stage("Await Code Analysis Result") {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}