pipeline {
    agent any

    tools {
        maven 'Maven 3.9.11'  // Adjust to your configured Maven version name in Jenkins
    }

    environment {
        SONAR_TOKEN = credentials('sonar-token') // Make sure you created this credential
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=shambhavimisra_jenkins-sonarcloud-demo -Dsonar.organization=shambhavimisra -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=$SONAR_TOKEN'
                }
            }
        }
    }
}
