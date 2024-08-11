node {
  stage('SCM') {
    git 'https://github.com/foo/bar.git'
  }
  stage('SonarQube analysis') {
    withSonarQubeEnv() { // Will pick the global server connection you have configured
      sh './gradlew sonar'
    }
  }
}

// pipeline {
//   agent {label 'linux'}
//   options {
//     buildDiscarder(logRotator(numToKeepStr: '5'))
//   }

//   stages {
//     stage('Scan'){
//       steps {
//         withSonarQubeEnv(installationName: 'SonarQube'){
//           // sh './mvnw clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
//           sh './gradlew sonarqube'
//         }
//       }
//     }
//   }  
// }

