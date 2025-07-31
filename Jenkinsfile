pipeline {
    agent any

    tools {
        maven 'Maven 3.9.11' // 🔁 MUST match name in Jenkins Global Tool Config
    }

    environment {
        // SONARQUBE env is configured via 'withSonarQubeEnv'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/shambhavimisra/jenkins-sonarcloud-demo.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') { // 🔁 MUST match name in "Manage Jenkins > Configure System > SonarQube Servers"
                    bat 'mvn sonar:sonar'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
