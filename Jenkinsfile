pipeline {
  agent any
  stages {
    stage('StaticCodeAnalisis') {
      agent {
        node {
          label 'ubuntu'
        }

      }
      steps {
        withSonarQubeEnv(installationName: 'SonarQube', credentialsId: 'b47ae889-5156-4183-8c75-1e8bcf1e0244') {
          sh '''pipeline {
    agent {
        node { label \'ubuntu\' }  // Run this pipeline on a node with the label \'ubuntu\'
    }
    stages {
        stage(\'Static Code Analysis\') {
            steps {
                withSonarQubeEnv(installationName: \'SonarQube\', credentialsId: \'SonarToken\') {
                    sh \'\'\'
                    # Run SonarQube Scanner
                    /path/to/sonar-scanner/bin/sonar-scanner \\
                    -Dsonar.projectVersion=1.0 \\
                    -Dsonar.projectKey=spring-app \\
                    -Dsonar.sources=src \\
                    -Dsonar.java.binaries=.
                    \'\'\'
                }
            }
        }
    }
    post {
        always {
            cleanWs()  // Clean up the workspace after the build
        }
    }
}
'''
            waitForQualityGate(credentialsId: 'b47ae889-5156-4183-8c75-1e8bcf1e0244', abortPipeline: true)
          }

        }
      }

    }
  }