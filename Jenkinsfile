pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'SonarQube' // Name of your SonarQube installation in Jenkins
        SONARQUBE_TOKEN = credentials('petJenkinsToken') // Credentials ID for SonarQube token
        SONARQUBE_URL = 'http://192.168.115.166:9000' // URL of your SonarQube server
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/kakybat/spring-petclinic.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQubeScanner') {
                    sh './gradlew sonarqube ' +
                       '-Dsonar.projectKey=spring-petclinic ' +
                       '-Dsonar.host.url=$SONARQUBE_URL ' +
                       '-Dsonar.login=$SONARQUBE_TOKEN ' +
                       '-Dsonar.projectName=spring-petclinic ' +
                       '-Dsonar.projectVersion=$BUILD_NUMBER'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                script {
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error "Pipeline aborted due to quality gate failure: ${qg.status}"
                    }
                }
            }
        }
    }
}
