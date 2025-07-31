pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }

    tools {
        sonarQubeScanner 'SonarScanner' // This must match the name configured in Jenkins → Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/shambhavimisra/jenkins-sonarcloud-demo.git', branch: 'main'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') { // This must match your name in "Configure System" for SonarQube server
                    sh '''
                        sonar-scanner \
                          -Dsonar.projectKey=shambhavimisra_jenkins-sonarcloud-demo \
                          -Dsonar.organization=shambhavimisra \
                          -Dsonar.sources=. \
                          -Dsonar.host.url=https://sonarcloud.io \
                          -Dsonar.login=$SONAR_TOKEN
                    '''
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
