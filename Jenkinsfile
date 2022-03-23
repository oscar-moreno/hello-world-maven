pipeline {

  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Build started'
        sh "mvn clean install"
        echo 'Build finished'
      }
    }
    stage('Code Analysis') {
      steps {
        echo 'Code analysis with SonarQube started'
        withSonarQubeEnv('sonarqube-local-training-lts') {
          sh "mvn sonar:sonar"
        }
        echo 'Code analysis with SonarQube finished'
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
