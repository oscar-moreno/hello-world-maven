pipeline {

  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Build started'
        withMaven(maven: 'maven-latest') {
          sh "mvn clean install"
        }
        echo 'Build finished'
      }
    }
    stage('Code Analysis') {
      steps {
        echo 'Code analysis with SonarQube started'
        withSonarQubeEnv('sonarqube-local-lts') {
          withMaven(maven: 'maven-latest') {
            sh "mvn sonar:sonar"
          }
        echo 'Code analysis with SonarQube finished'
        }
      }
    }
    stage("Quality Gate") {
      steps {
        timeout(time: 5, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
    stage("Deploy"){
      steps{
        echo 'Deploy app'
      }
    }
  }
}
