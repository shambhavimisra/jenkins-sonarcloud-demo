pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }

    tools {
        sonarQubeScanner 'SonarScanner'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/shambhavimisra/jenkins-sonarcloud-demo.git', branch: 'main'
            }
        }

        stage('SonarCloud Scan') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    sh 'sonar-scanner -Dsonar.login=$SONAR_TOKEN'
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
